# Tool Policy Reference

Quick reference for tool restrictions, profiles, and sandbox configuration.

---

## Tool Profile Presets

Profiles provide a base set of allowed tools. Use `profile` as a starting point, then refine with `alsoAllow` and `deny`.

| Profile | Description |
|---------|-------------|
| `minimal` | Bare minimum tools for read-only operation |
| `coding` | Tools oriented toward code reading, writing, and execution |
| `messaging` | Tools oriented toward message sending and channel interaction |
| `full` | All available tools enabled |

---

## Global Tool Policy (tools section)

The top-level `tools` section in `openclaw.json` sets global defaults for all agents:

```json5
{
  tools: {
    profile: "coding",             // base preset: "minimal" | "coding" | "messaging" | "full"
    allow: ["read", "write"],      // explicit allowlist (overrides profile if set)
    alsoAllow: ["browser"],        // additive — merged into allow/profile allowlist
    deny: ["gateway"],             // denylist — always wins over allow

    // Per-provider or per-model overrides
    byProvider: {
      "openai": {
        allow: ["read", "exec"],
        deny: ["write"],
      },
      "openai/gpt-4o": {
        alsoAllow: ["browser"],
      },
    },

    // Exec tool configuration
    exec: {
      host: "sandbox",            // "sandbox" | "gateway" | "node"
      security: "allowlist",      // "deny" | "allowlist" | "full"
      ask: "on-miss",             // "off" | "on-miss" | "always"
      node: "my-node",            // default node binding for exec.host=node
      pathPrepend: ["/opt/bin"],   // directories prepended to PATH
      safeBins: ["cat", "ls"],    // stdin-only binaries exempt from allowlist
      backgroundMs: 5000,         // ms before auto-backgrounding
      timeoutSec: 300,            // seconds before auto-killing
    },

    // Web tools
    web: {
      search: {
        enabled: true,
        provider: "brave",        // "brave" | "perplexity" | "grok"
        maxResults: 5,
      },
      fetch: {
        enabled: true,
        maxChars: 10000,
        timeoutSeconds: 30,
      },
    },

    // Agent-to-agent messaging
    agentToAgent: {
      enabled: true,
      allow: ["agent-a", "agent-b"],
    },

    // Sub-agent tool policy defaults (global)
    subagents: {
      model: "anthropic/claude-sonnet-4",
      tools: {
        allow: ["read", "exec", "write", "edit"],  // restrict sub-agents to these tools
        deny: ["browser", "gateway"],               // OR deny specific tools
      },
    },

    // Sandbox tool policy defaults
    sandbox: {
      tools: {
        allow: ["read", "exec"],
        deny: ["gateway"],
      },
    },
  },
}
```

---

## Per-Agent Tool Configuration

Each agent entry can override the global tool policy. The agent-level `tools` block has the same shape as the global one, plus `elevated` and `sandbox` overrides:

```json5
{
  agents: {
    list: [
      {
        id: "{agent-id}",
        tools: {
          // Base profile preset
          profile: "messaging",      // "minimal" | "coding" | "messaging" | "full"

          // Explicit allowlist (overrides profile)
          allow: ["{tool1}", "{tool2}"],

          // Additive allowlist (merged into allow/profile)
          alsoAllow: ["{tool3}"],

          // Denylist (always wins)
          deny: ["{tool4}"],

          // Per-provider overrides at agent level
          byProvider: {
            "anthropic": {
              deny: ["exec"],
            },
          },

          // Per-agent exec configuration
          exec: {
            host: "gateway",        // "sandbox" | "gateway" | "node"
            security: "full",       // "deny" | "allowlist" | "full"
          },

          // Per-agent elevated exec gate
          elevated: {
            enabled: true,
            allowFrom: {
              whatsapp: ["1234567890"],
              telegram: [123456789],
            },
          },

          // Sandbox tool restrictions for this agent
          sandbox: {
            tools: {
              allow: ["read"],
              deny: ["write", "edit"],
            },
          },
        },
      },
    ],
  },
}
```

**Approach options for per-agent tools:**
- **Profile-based** (recommended): Set `profile` as a starting point, then use `alsoAllow` and `deny` to customize
- **Allow-list** (restrictive): Only specify tools the agent CAN use via `allow`
- **Deny-list** (permissive): Only specify tools the agent CANNOT use via `deny`
- **Default** (no restrictions): Omit the `tools` block entirely; agent gets the global tool set

---

## Default Sub-Agent Tool Restrictions (Built-In)

Sub-agents get all tools EXCEPT the following, which are denied by default:

| Denied by Default | Reason |
|-------------------|--------|
| `sessions_list` | Session management -- main agent orchestrates |
| `sessions_history` | Session management -- main agent orchestrates |
| `sessions_send` | Session management -- main agent orchestrates |
| `sessions_spawn` | No nested spawning |
| `gateway` | System admin -- dangerous from sub-agent |
| `agents_list` | System admin |
| `whatsapp_login` | Interactive setup |
| `session_status` | Scheduling -- main agent coordinates |
| `cron` | Scheduling -- main agent coordinates |
| `memory_search` | Pass info in spawn prompt instead |
| `memory_get` | Pass info in spawn prompt instead |

**Sub-agents CAN by default:** `read`, `write`, `edit`, `exec`, `apply_patch`, `browser`, `process`, and others.

---

## Global Sub-Agent Tool Overrides

Override the built-in sub-agent tool restrictions globally via `tools.subagents.tools`:

```json5
{
  tools: {
    subagents: {
      model: "minimax/MiniMax-M2.1",   // default model for sub-agents
      tools: {
        // Restrict sub-agents to ONLY these tools:
        allow: ["read", "exec", "write", "edit"],
        // OR deny additional tools:
        deny: ["browser", "firecrawl"],
      },
    },
  },
}
```

---

## Sandbox Configuration

**Modes:**
- `off` -- No sandboxing (host access)
- `non-main` -- Sandbox non-main sessions only
- `all` -- Always sandboxed

**Workspace Access:**
- `none` -- Do not mount agent workspace; use sandbox workspace
- `ro` -- Mount agent workspace read-only; disables write/edit tools
- `rw` -- Mount agent workspace read/write; enables write/edit tools

**Session Tools Visibility:**
- `spawned` -- Only allow session tools to target sessions spawned from this session (default)
- `all` -- Allow session tools to target any session

**Scope:**
- `session` -- One container per session
- `agent` -- One container per agent
- `shared` -- All agents share one container

```json5
{
  agents: {
    list: [
      {
        id: "{agent-id}",
        sandbox: {
          mode: "all",                          // "off" | "non-main" | "all"
          workspaceAccess: "rw",                // "none" | "ro" | "rw"
          sessionToolsVisibility: "spawned",    // "spawned" | "all"
          scope: "agent",                       // "session" | "agent" | "shared"
          docker: {
            setupCommand: "apt-get update && apt-get install -y git",
          },
        },
      },
    ],
  },
}
```

Global sandbox defaults live in `agents.defaults.sandbox` with the same shape.

---

## Sub-Agent Model Configuration

```json5
{
  agents: {
    defaults: {
      subagents: {
        maxConcurrent: 4,            // max concurrent sub-agent runs (default: 1)
        archiveAfterMinutes: 60,     // auto-archive after idle minutes (default: 60)
        model: "minimax/MiniMax-M2.1",  // default sub-agent model
        thinking: "low",             // default thinking level
      },
    },
    list: [
      {
        id: "{agent-id}",
        subagents: {
          model: "anthropic/claude-sonnet-4",  // per-agent sub-agent model override
        },
      },
    ],
  },
}
```
