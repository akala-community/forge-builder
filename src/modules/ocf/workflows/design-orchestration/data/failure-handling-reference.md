# Failure Handling Reference

Quick reference for failure scenarios and prevention strategies during orchestration design.

---

## Common Failure Scenarios

1. **Sub-agent timeout** — spawned task takes too long
2. **Sub-agent error** — spawned task fails with an error
3. **Send timeout** — sessions_send doesn't get a response in time
4. **Send error** — target agent session is unavailable
5. **Gateway restart** — pending announces/archives are lost
6. **Model error** — LLM API returns an error
7. **Loop detection** — agents trigger infinite communication cycles

---

## Sub-Agent Failure Config

**Timeout:**
- `runTimeoutSeconds`: Set per spawn (0 = no limit)
- `cleanup`: `"delete"` for ephemeral tasks, `"keep"` for important ones

**Recommended patterns:**
- Set `runTimeoutSeconds` for all non-trivial tasks
- Include error context in spawn prompts so sub-agents can self-correct
- Best-effort announce: If gateway restarts, pending announces are lost

---

## Send Failure Config

**Timeout:**
- `timeoutSeconds`: Set per send (0 = fire-and-forget, >0 = wait)

**Reply limits:**
- `maxPingPongTurns`: Cap reply rounds (0-5, default 5)
- `REPLY_SKIP`: Agent reply to end conversation early
- `ANNOUNCE_SKIP`: Skip posting announce to channel

---

## Loop Prevention Strategies

1. **Ping-pong limits:** Set `maxPingPongTurns` to cap reply rounds
2. **Send policy rules:** Deny specific channel/chatType combinations
3. **No nested spawning:** Sub-agents CANNOT spawn sub-agents (built-in)
4. **Mention gating:** Agents only respond to direct @mentions in groups
5. **Session-level send policy:** Override per-session

### Send Policy Config

```json5
{
  session: {
    agentToAgent: {
      maxPingPongTurns: 3,
    },
    sendPolicy: {
      rules: [
        { match: { channel: 'discord', chatType: 'group' }, action: 'deny' },
      ],
      default: 'allow',
    },
  },
}
```

---

## Recovery Strategies

**Gateway restart recovery:**
- Pending sub-agent announces are lost
- Auto-archive timers reset
- Active sessions continue from last checkpoint

**Recommended recovery patterns:**
- Design idempotent sub-agent tasks (safe to re-run)
- Include diagnostic prompts in agent workspaces
- Use session history for recovery context
