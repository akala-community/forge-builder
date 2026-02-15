# OpenClaw Orchestration Reference

Quick reference for orchestration primitives used during the design workflow.

---

## Agent Entry Schema

Each agent is defined in the `agents.list` array of `openclaw.json`. Every agent gets its own workspace, state directory, and session store.

```json5
{
  agents: {
    list: [
      {
        id: "agent-id",           // (required) unique agent identifier
        default: true,            // mark as the default agent for unmatched messages
        name: "Display Name",     // optional display name
        workspace: "/path/to/workspace",  // working directory for agent runs
        agentDir: "/path/to/agent",       // directory containing workspace files (SOUL.md, etc.)

        // Model selection — string shorthand or object with fallbacks
        model: "anthropic/claude-sonnet-4",
        // OR:
        model: {
          primary: "anthropic/claude-sonnet-4",
          fallbacks: ["openai/gpt-4o"],
        },

        // Optional skill allowlist (omit = all skills; empty array = none)
        skills: ["daily-summary", "code-review"],

        // Vector memory search overrides
        memorySearch: {
          enabled: true,
          sources: ["memory", "sessions"],
          provider: "openai",
        },

        // Human-like delay between block replies
        humanDelay: {
          mode: "natural",   // "off" | "natural" | "custom"
          minMs: 800,
          maxMs: 2500,
        },

        // Per-agent heartbeat overrides (inherits from agents.defaults.heartbeat)
        heartbeat: {
          every: "30m",
          target: "last",
          model: "anthropic/claude-sonnet-4",
        },

        // Agent identity (used in response prefixes, avatars)
        identity: {
          name: "Cleo",
          emoji: "🧠",
          avatar: "avatar.png",   // workspace-relative, URL, or data URI
          theme: "dark",
        },

        // Group chat behavior
        groupChat: {
          mentionPatterns: ["@cleo", "@cleobot"],
          historyLimit: 50,
        },

        // Sub-agent spawning configuration
        subagents: {
          allowAgents: ["researcher", "coder"],  // or ["*"] for any
          model: "anthropic/claude-sonnet-4",     // default model for spawned sub-agents
          // OR: model: { primary: "...", fallbacks: ["..."] }
        },

        // Sandbox isolation
        sandbox: {
          mode: "all",                // "off" | "non-main" | "all"
          workspaceAccess: "rw",      // "none" | "ro" | "rw"
          sessionToolsVisibility: "spawned",  // "spawned" | "all"
          scope: "agent",             // "session" | "agent" | "shared"
          docker: {
            setupCommand: "apt-get update && apt-get install -y git",
          },
        },

        // Tool policy for this agent
        tools: {
          profile: "coding",           // "minimal" | "coding" | "messaging" | "full"
          allow: ["read", "exec"],     // explicit allowlist (overrides profile)
          alsoAllow: ["browser"],      // additive — merged into allow/profile
          deny: ["gateway"],           // denylist (wins over allow)
          byProvider: {                // per-provider/model overrides
            "openai": { deny: ["exec"] },
          },
          exec: {
            host: "sandbox",           // "sandbox" | "gateway" | "node"
            security: "allowlist",     // "deny" | "allowlist" | "full"
          },
          web: {
            search: { enabled: true, provider: "brave" },
          },
        },
      },
    ],
  },
}
```

---

## Binding Schema (Channel Routing)

Bindings route inbound messages to agents. Most-specific match wins.

**Match Priority (highest to lowest):**
1. `peer` match (exact DM/group/channel id)
2. `guildId` (Discord server)
3. `teamId` (Slack workspace)
4. `accountId` match for a channel
5. Channel-level match (`accountId: "*"`)
6. Fallback to default agent (`default: true`)

```json5
{
  bindings: [
    // Peer-level (most specific)
    {
      agentId: "ops",
      match: {
        channel: "whatsapp",
        peer: { kind: "group", id: "12036...@g.us" },
      },
    },
    // Account-level
    {
      agentId: "work",
      match: { channel: "whatsapp", accountId: "biz" },
    },
    // Guild-level (Discord)
    {
      agentId: "community",
      match: { channel: "discord", guildId: "123456789" },
    },
    // Team-level (Slack)
    {
      agentId: "team",
      match: { channel: "slack", teamId: "T01234567" },
    },
    // Channel-level (least specific)
    {
      agentId: "main",
      match: { channel: "telegram" },
    },
  ],
}
```

---

## sessions_spawn (Sub-Agents)

Spawn background tasks in isolated sessions. Non-blocking.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `task` | string | yes | What the sub-agent should do |
| `label` | string | no | Short identifier for the spawned session |
| `agentId` | string | no | Spawn under a different agent (must be in `allowAgents`) |
| `model` | string | no | Override model for the sub-agent run |
| `thinking` | string | no | Override thinking level (off, low, medium, high) |
| `runTimeoutSeconds` | number | no | Abort after N seconds |
| `timeoutSeconds` | number | no | Legacy alias for `runTimeoutSeconds` |
| `cleanup` | string | no | `"delete"` or `"keep"` (default: `"keep"`) |

**Cross-Agent Spawning:**

The spawning agent must declare which other agent IDs it can spawn under:

```json5
{
  agents: {
    list: [
      {
        id: "orchestrator",
        subagents: {
          allowAgents: ["researcher", "coder"],  // or ["*"] for any
          model: "anthropic/claude-sonnet-4",     // default model for sub-agents
        },
      },
    ],
  },
}
```

**Constraints:**
- Sub-agents cannot spawn sub-agents (no nesting)
- Max concurrent governed by `agents.defaults.subagents.maxConcurrent` (default: 1)
- Auto-archive after `agents.defaults.subagents.archiveAfterMinutes` (default: 60)

---

## sessions_send (Agent-to-Agent Messaging)

Send a message into another session. Supports sync and fire-and-forget.

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `sessionKey` | string | no | Target session key |
| `label` | string | no | Target session by label |
| `agentId` | string | no | Target agent ID |
| `message` | string | yes | Message content |
| `timeoutSeconds` | number | no | Wait for reply (0 = fire-and-forget) |

**Reply Ping-Pong:**
- After primary run, agents alternate replies
- Reply `REPLY_SKIP` to stop early
- Max turns: `session.agentToAgent.maxPingPongTurns` (0-5, default 5)

**Agent-to-Agent must be enabled:**

```json5
{
  tools: {
    agentToAgent: {
      enabled: true,
      allow: ["agent-a", "agent-b"],
    },
  },
}
```

---

## Sub-Agent Defaults (agents.defaults.subagents)

Configure defaults for all spawned sub-agents:

```json5
{
  agents: {
    defaults: {
      subagents: {
        maxConcurrent: 4,            // max concurrent sub-agent runs (default: 1)
        archiveAfterMinutes: 60,     // auto-archive idle sub-agent sessions
        model: "anthropic/claude-sonnet-4",  // default model for sub-agents
        thinking: "low",             // default thinking level
      },
    },
  },
}
```

Per-agent overrides in the agent entry's `subagents` block (model only):

```json5
{
  agents: {
    list: [
      {
        id: "coder",
        subagents: {
          model: "openai/gpt-4o",  // per-agent sub-agent model override
        },
      },
    ],
  },
}
```

---

## Per-Agent Tool Policy

```json5
{
  agents: {
    list: [
      {
        id: "restricted-agent",
        tools: {
          profile: "minimal",                  // base preset
          alsoAllow: ["browser"],              // additive on top of profile
          deny: ["write", "edit", "gateway"],  // deny always wins
          exec: {
            host: "sandbox",
            security: "allowlist",
          },
        },
        sandbox: {
          mode: "all",
          scope: "agent",
        },
      },
    ],
  },
}
```

---

## Session Send Policy

```json5
{
  session: {
    sendPolicy: {
      rules: [
        { match: { channel: "discord", chatType: "group" }, action: "deny" },
      ],
      default: "allow",
    },
  },
}
```
