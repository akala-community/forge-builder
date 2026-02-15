# Boundary Rules Configuration Reference

## Architecture

Boundaries in OpenClaw operate at two distinct levels:

1. **Soft boundaries (prompt-based):** Behavioral directives in `SOUL.md` and `AGENTS.md` that the model follows via instruction-following. These are best-effort and depend on model capability.
2. **Hard boundaries (runtime-enforced):** Configuration fields in `openclaw.json` that are enforced by the runtime engine, Docker containers, or channel providers. These cannot be bypassed by the model.

Production deployments should use hard boundaries for security-critical rules and soft boundaries for tone, scope, and behavioral guidance.

---

## Soft Boundaries (SOUL.md Directives)

The `SOUL.md` file defines the agent's persona, values, and behavioral limits. Add a `## Boundaries` section to establish prompt-enforced guardrails.

### Example SOUL.md Boundaries Section

```markdown
## Boundaries

- Private things stay private. Never repeat credentials, API keys, or passwords.
- Ask before acting externally. Do not send messages, make API calls, or modify
  files outside your workspace without explicit user approval.
- Stay within your domain. If a request falls outside your expertise, say so and
  suggest who or what might help instead.
- Escalate when uncertain. If you are unsure whether an action is safe or
  appropriate, ask the user before proceeding.
- Do not fabricate. Never invent file paths, function names, API endpoints,
  or tool outputs. If you do not know, say so.
```

### Safety Rules in AGENTS.md

Operational safety rules that are more procedural than persona-driven belong in `AGENTS.md`:

```markdown
## Safety

- Never execute shell commands that delete files recursively without explicit
  user confirmation of the exact path
- Do not commit or push to git without user approval
- Do not modify configuration files (openclaw.json, .env) without showing
  the diff first
- When handling user data, do not log PII to daily notes
```

---

## Hard Boundaries (Runtime Configuration)

These fields in `openclaw.json` are enforced by the runtime and cannot be overridden by model behavior.

### Channel Access Control

Controls who can interact with the agent through messaging channels.

```json
{
  "channels": {
    "whatsapp": {
      "dmPolicy": "pairing",
      "allowFrom": ["+15551234567", "+15559876543"],
      "groupPolicy": "allowlist",
      "groupAllowFrom": ["+15551111111"]
    }
  }
}
```

**`dmPolicy`** (type: `DmPolicy`)

| Value | Behavior |
|-------|----------|
| `"pairing"` | New users must complete a pairing flow before chatting (default) |
| `"allowlist"` | Only phone numbers in `allowFrom` can send DMs |
| `"open"` | Anyone can send DMs without approval |
| `"disabled"` | DMs are blocked entirely |

**`allowFrom`** (type: `string[]`)

E.164 format phone numbers permitted to send direct messages. Only enforced when `dmPolicy` is `"allowlist"`. Also used as a base allowlist for group senders when `groupPolicy` is `"allowlist"`.

**`groupPolicy`** (type: `GroupPolicy`)

| Value | Behavior |
|-------|----------|
| `"open"` | Groups bypass allowFrom; only mention-gating applies |
| `"disabled"` | Block all group messages entirely |
| `"allowlist"` | Only allow group messages from senders in `groupAllowFrom` / `allowFrom` |

These same fields exist for Telegram, Discord, IRC, and other channel types with provider-appropriate ID formats.

### Sandbox Isolation

Controls the execution environment for agent sessions.

```json
{
  "agents": {
    "defaults": {
      "sandbox": {
        "mode": "non-main",
        "workspaceAccess": "ro",
        "scope": "session",
        "docker": {
          "image": "openclaw-sandbox:latest"
        }
      }
    }
  }
}
```

**`sandbox.mode`**

| Value | Behavior |
|-------|----------|
| `"off"` | No sandboxing; agent runs on the host |
| `"non-main"` | Sandbox all sessions except the main session |
| `"all"` | Sandbox every session including main |

**`sandbox.workspaceAccess`**

| Value | Behavior |
|-------|----------|
| `"none"` | Do not mount agent workspace; use a sandbox-local workspace |
| `"ro"` | Mount agent workspace read-only; write/edit tools are disabled |
| `"rw"` | Mount agent workspace read/write; write/edit tools are enabled |

**`sandbox.scope`**

| Value | Behavior |
|-------|----------|
| `"session"` | Each session gets its own container/workspace |
| `"agent"` | All sessions for an agent share a container/workspace |
| `"shared"` | All agents share a container/workspace |

**`sandbox.sessionToolsVisibility`**

| Value | Behavior |
|-------|----------|
| `"spawned"` | Sandboxed sessions can only target sessions they spawned (default) |
| `"all"` | Sandboxed sessions can target any session |

### Exec Tool Security

Controls whether the agent can execute shell commands.

```json
{
  "tools": {
    "exec": {
      "security": "allowlist",
      "host": "sandbox",
      "ask": "on-miss"
    }
  }
}
```

**`tools.exec.security`**

| Value | Behavior |
|-------|----------|
| `"deny"` | Shell execution is completely blocked (default) |
| `"allowlist"` | Only pre-approved commands can run |
| `"full"` | Any shell command can run (use with extreme caution) |

**`tools.exec.host`**

| Value | Behavior |
|-------|----------|
| `"sandbox"` | Execute in sandbox container (default) |
| `"gateway"` | Execute on the gateway host |
| `"node"` | Execute on a remote node |

**`tools.exec.ask`**

| Value | Behavior |
|-------|----------|
| `"off"` | Never ask for approval |
| `"on-miss"` | Ask when command is not in the allowlist |
| `"always"` | Always ask before executing any command |

### Tool Policies

Controls which tools the agent can use.

```json
{
  "tools": {
    "profile": "minimal",
    "allow": ["web_search"],
    "deny": ["exec_command"],
    "alsoAllow": ["weather"]
  }
}
```

Per-agent overrides in `agents.list[].tools` can further restrict (but not expand beyond) the global tool policy.

**Profiles:**

| Profile | Description |
|---------|-------------|
| `"minimal"` | Basic read and search tools only |
| `"coding"` | File read/write, restricted shell, search |
| `"messaging"` | Channel send, user lookup, search |
| `"full"` | All tools available |

**Priority order:** `deny` > `allow` / `alsoAllow` > `profile` defaults.

### Group Chat Mention Gating

Controls when the agent responds in group chats.

```json
{
  "messages": {
    "groupChat": {
      "mentionPatterns": ["@myagent", "hey agent"]
    }
  }
}
```

Per-agent mention patterns can also be set in `agents.list[].groupChat.mentionPatterns`.

### Elevated Permissions

Controls whether users can grant temporary elevated exec access.

```json
{
  "tools": {
    "elevated": {
      "enabled": true,
      "allowFrom": {
        "whatsapp": ["+15551234567"],
        "telegram": ["123456789"]
      }
    }
  }
}
```

---

## Soft vs. Hard Boundary Summary

| Boundary Type | Location | Enforcement | Use For |
|---------------|----------|-------------|---------|
| Persona / tone | SOUL.md | Model instruction-following | Voice, style, personality |
| Scope / domain | SOUL.md ## Boundaries | Model instruction-following | Staying in lane |
| Error handling | AGENTS.md ## Safety | Model instruction-following | Operational procedures |
| DM access | `channels.*.dmPolicy` | Runtime engine | Who can talk to the agent |
| Sender allowlist | `channels.*.allowFrom` | Runtime engine | Identity verification |
| Shell execution | `tools.exec.security` | Runtime engine | Command execution control |
| Tool availability | `tools.profile` / `deny` | Runtime engine | Feature gating |
| File system access | `sandbox.workspaceAccess` | Docker / OS | Read/write isolation |
| Container isolation | `sandbox.mode` | Docker | Process isolation |
| Group response gating | `mentionPatterns` | Runtime engine | Noise reduction |

### Production Recommendations

1. **Never rely solely on soft boundaries for security.** If an action is dangerous, deny it in config.
2. **Use `sandbox.mode: "all"` with `workspaceAccess: "ro"` or `"none"`** for agents that should not modify the host filesystem.
3. **Set `tools.exec.security: "deny"`** unless the agent specifically needs shell access, then use `"allowlist"`.
4. **Set `dmPolicy: "pairing"` or `"allowlist"`** for any public-facing channel.
5. **Layer soft boundaries on top of hard ones.** Use `SOUL.md` to guide the model's judgment in ambiguous cases that hard config cannot anticipate.
