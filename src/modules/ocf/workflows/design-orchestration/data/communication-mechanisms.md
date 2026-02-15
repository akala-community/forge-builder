# Communication Mechanisms Reference

Quick reference for spawn vs send decisions during orchestration design.

---

## sessions_spawn (Sub-Agents)

- Creates an isolated background session
- Non-blocking -- main agent continues working
- Sub-agent announces results back when done
- Best for: Task delegation, background research, parallel work
- Limitation: Sub-agents CANNOT spawn their own sub-agents (no nesting)
- Limitation: Sub-agents have restricted tool access by default

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

## sessions_send (Agent-to-Agent Messaging)

- Sends a message into another agent's session
- Can be sync (wait for reply) or fire-and-forget (`timeoutSeconds: 0`)
- Supports reply ping-pong (up to 5 rounds, configurable)
- Must be explicitly enabled in config
- Best for: Peer-to-peer communication, handoffs, notifications

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `sessionKey` | string | no | Target session key |
| `label` | string | no | Target session by label |
| `agentId` | string | no | Target agent ID |
| `message` | string | yes | Message content |
| `timeoutSeconds` | number | no | Wait for reply (0 = fire-and-forget) |

## Key Decision Framework

- Is it a parent-to-child task delegation? -> **spawn**
- Is it peer-to-peer collaboration? -> **send**
- Does it need background processing? -> **spawn**
- Does it need back-and-forth dialogue? -> **send**
- Is it a one-way notification? -> **send** (fire-and-forget, `timeoutSeconds: 0`)

---

## Cross-Agent Spawn Permissions

For agents that spawn sub-agents under a DIFFERENT agent ID, the spawning agent must declare which targets are allowed in its `subagents.allowAgents` array:

```json5
{
  agents: {
    list: [
      {
        id: "{spawning-agent}",
        subagents: {
          allowAgents: ["{target-agent-1}", "{target-agent-2}"],  // or ["*"]
          model: "anthropic/claude-sonnet-4",  // optional default model
        },
      },
    ],
  },
}
```

## Sub-Agent Defaults (agents.defaults.subagents)

Global sub-agent configuration lives in `agents.defaults.subagents`:

```json5
{
  agents: {
    defaults: {
      subagents: {
        maxConcurrent: 4,            // max concurrent sub-agent runs (default: 1)
        archiveAfterMinutes: 60,     // auto-archive after idle minutes (default: 60)
        model: "minimax/MiniMax-M2.1",  // default model for all sub-agents
        thinking: "low",             // default thinking level
      },
    },
  },
}
```

Per-agent model override (in the agent entry):

```json5
{
  agents: {
    list: [
      {
        id: "{agent-id}",
        subagents: {
          model: "anthropic/claude-sonnet-4",  // overrides agents.defaults.subagents.model
        },
      },
    ],
  },
}
```

## Agent-to-Agent Messaging Config

For agents using `sessions_send`:

```json5
{
  tools: {
    agentToAgent: {
      enabled: true,
      allow: ["{agent-a}", "{agent-b}"],
    },
  },
}
```

**Ping-pong settings:**
- `session.agentToAgent.maxPingPongTurns`: How many reply rounds? (0-5, default 5)
- Agents can reply `REPLY_SKIP` to end conversations early
- `ANNOUNCE_SKIP` skips posting announce to target channel

## Session Key Patterns

- Main DMs: `agent:{agentId}:{mainKey}`
- Groups: `agent:{agentId}:{channel}:group:{id}`
- Sub-agents: `agent:{agentId}:subagent:{uuid}`
- Cron: `cron:{job.id}`
