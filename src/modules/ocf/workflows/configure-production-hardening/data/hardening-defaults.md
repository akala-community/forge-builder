# Production Hardening Defaults and Reference

Reference data for the configure-production-hardening workflow. All configuration fields, types, and defaults are sourced directly from the OpenClaw codebase (`src/config/types.*.ts`).

---

## Memory Search

Vector memory search is configured via `agents.defaults.memorySearch`. The type is `MemorySearchConfig` from `src/config/types.tools.ts`.

### Configuration

```json
{
  "agents": {
    "defaults": {
      "memorySearch": {
        "enabled": true,
        "provider": "openai",
        "model": "text-embedding-3-small",
        "sources": ["memory"],
        "store": {
          "driver": "sqlite",
          "vector": { "enabled": true },
          "cache": { "enabled": true }
        },
        "fallback": "local",
        "chunking": { "tokens": 512, "overlap": 64 },
        "sync": {
          "onSessionStart": true,
          "onSearch": true,
          "watch": false
        },
        "query": {
          "maxResults": 10,
          "minScore": 0.3,
          "hybrid": {
            "enabled": true,
            "vectorWeight": 0.7,
            "textWeight": 0.3
          }
        }
      }
    }
  }
}
```

### Key Fields

| Field | Type | Description |
|-------|------|-------------|
| `enabled` | `boolean` | Enable vector memory search (default: true) |
| `provider` | `"openai" \| "gemini" \| "local" \| "voyage"` | Embedding provider |
| `model` | `string` | Embedding model id |
| `sources` | `("memory" \| "sessions")[]` | What to index (default: `["memory"]`) |
| `extraPaths` | `string[]` | Additional directories or .md files to index |
| `store.driver` | `"sqlite"` | Index storage driver |
| `store.vector.enabled` | `boolean` | Enable sqlite-vec extension (default: true) |
| `store.cache.enabled` | `boolean` | Cache chunk embeddings (default: true) |
| `fallback` | `"openai" \| "gemini" \| "local" \| "voyage" \| "none"` | Fallback when embeddings fail |
| `chunking.tokens` | `number` | Chunk size in tokens |
| `chunking.overlap` | `number` | Overlap between chunks |
| `sync.onSessionStart` | `boolean` | Re-sync index at session start |
| `sync.onSearch` | `boolean` | Re-sync before search queries |
| `sync.watch` | `boolean` | Watch filesystem for changes |
| `query.maxResults` | `number` | Max search results returned |
| `query.minScore` | `number` | Minimum similarity score |
| `query.hybrid.enabled` | `boolean` | Enable BM25 + vector hybrid search (default: true) |

### Workspace Artifacts

| File | Purpose |
|------|---------|
| `MEMORY.md` | Long-term curated storage; agents distill daily logs here |
| `memory/YYYY-MM-DD.md` | Daily append-only session logs |
| `USER.md` | User profile (name, timezone, preferences) |

### Per-Role Recommendations

| Agent Role | Enabled | Sources | Notes |
|------------|---------|---------|-------|
| Primary assistant | true | `["memory"]` | Full memory for personalized interactions |
| Specialist | true | `["memory"]` | Recalls past resolutions |
| Monitor | true | `["memory"]` | Recalls context but directives should limit capture |
| Stateless tool | false | -- | No persistence needed |

---

## Tool Policies

Tool policies use a "Profile + Exception" model. Type: `ToolPolicyConfig` / `AgentToolsConfig` from `src/config/types.tools.ts`.

### Configuration

```json
{
  "tools": {
    "profile": "coding",
    "allow": ["camera.*"],
    "deny": ["exec_command"],
    "alsoAllow": ["weather"],
    "exec": {
      "host": "sandbox",
      "security": "deny",
      "ask": "on-miss",
      "safeBins": ["cat", "ls", "grep"],
      "backgroundMs": 30000,
      "timeoutSec": 120
    },
    "web": {
      "search": {
        "enabled": true,
        "provider": "brave",
        "maxResults": 5,
        "timeoutSeconds": 10,
        "cacheTtlMinutes": 30
      },
      "fetch": {
        "enabled": true,
        "maxChars": 30000,
        "timeoutSeconds": 15,
        "readability": true
      }
    },
    "elevated": {
      "enabled": true,
      "allowFrom": {
        "whatsapp": ["+15551234567"]
      }
    }
  }
}
```

### Profiles

| Profile | Description | Includes |
|---------|-------------|----------|
| `"minimal"` | Bare minimum | Basic read, search |
| `"coding"` | Development-focused | File read/write, restricted shell, search |
| `"messaging"` | Communication-focused | Channel send, user lookup, search |
| `"full"` | All tools available | Everything except explicitly denied |

### Priority

`deny` (highest) > `allow` / `alsoAllow` > `profile` defaults (lowest).

- `allow`: explicit allows that override profile denials
- `alsoAllow`: additive permissions on top of profile (does not replace existing allow)
- `deny`: explicit denies that override everything

### Exec Tool Fields

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `host` | `"sandbox" \| "gateway" \| "node"` | `"sandbox"` | Where commands execute |
| `security` | `"deny" \| "allowlist" \| "full"` | `"deny"` | Execution security mode |
| `ask` | `"off" \| "on-miss" \| "always"` | `"on-miss"` | Approval prompt behavior |
| `safeBins` | `string[]` | -- | Stdin-only binaries that bypass allowlist |
| `backgroundMs` | `number` | -- | Auto-background after N ms |
| `timeoutSec` | `number` | -- | Auto-kill after N seconds |
| `notifyOnExit` | `boolean` | -- | Emit event when backgrounded exec exits |

### Per-Agent Overrides

Per-agent tool policies are set in `agents.list[].tools` and can only further restrict the global policy:

```json
{
  "agents": {
    "list": [
      {
        "id": "monitor",
        "tools": {
          "profile": "minimal",
          "deny": ["write_file", "exec_command"]
        }
      }
    ]
  }
}
```

---

## Failover

Model failover is configured via `agents.defaults.model` and `agents.defaults.imageModel`. Type: `AgentModelListConfig` from `src/config/types.agent-defaults.ts`.

### Configuration

```json
{
  "agents": {
    "defaults": {
      "model": {
        "primary": "anthropic/claude-sonnet-4-20250514",
        "fallbacks": ["openai/gpt-4o", "anthropic/claude-haiku-4-20250514"]
      },
      "imageModel": {
        "primary": "openai/gpt-4o",
        "fallbacks": ["anthropic/claude-sonnet-4-20250514"]
      },
      "timeoutSeconds": 30,
      "models": {
        "ollama/llama3": {
          "alias": "local",
          "streaming": false
        }
      }
    }
  }
}
```

### Fields

| Field | Type | Description |
|-------|------|-------------|
| `model.primary` | `string` | Primary model in `"provider/model"` format |
| `model.fallbacks` | `string[]` | Fallback models tried in order on failure |
| `imageModel.primary` | `string` | Primary image-capable model |
| `imageModel.fallbacks` | `string[]` | Fallback image models |
| `timeoutSeconds` | `number` | Per-request timeout |
| `models` | `Record<string, AgentModelEntryConfig>` | Model catalog with aliases and params |

### Retry

Retry logic is **not user-configurable**. It is hardcoded in `src/infra/retry-policy.ts`. Only channel-specific delivery retries (Discord: 3 attempts, Telegram: 3 attempts) have defaults. Model failover across providers is handled by `src/agents/model-fallback.ts` using auth profile rotation.

---

## Observability (Heartbeat)

Heartbeat provides cron-style proactive agent check-ins. Configured via `agents.defaults.heartbeat`.

### Configuration

```json
{
  "agents": {
    "defaults": {
      "heartbeat": {
        "every": "1h",
        "activeHours": {
          "start": "09:00",
          "end": "17:00",
          "timezone": "user"
        },
        "model": "anthropic/claude-haiku-4-20250514",
        "prompt": "Check in: review pending tasks, surface anything needing attention.",
        "target": "last",
        "session": "main",
        "ackMaxChars": 30,
        "includeReasoning": false
      }
    }
  }
}
```

### Fields

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `every` | `string` | `"30m"` | Heartbeat interval (duration string: ms, s, m, h) |
| `activeHours.start` | `string` | -- | Start time (24h, HH:MM), inclusive |
| `activeHours.end` | `string` | -- | End time (24h, HH:MM), exclusive; use `"24:00"` for EOD |
| `activeHours.timezone` | `string` | `"user"` | `"user"`, `"local"`, or IANA TZ id |
| `model` | `string` | -- | Model override for heartbeat runs |
| `prompt` | `string` | *(reads HEARTBEAT.md)* | Override heartbeat prompt body |
| `target` | `"last" \| "none" \| ChannelId` | -- | Delivery target |
| `to` | `string` | -- | Delivery override (E.164, chat id) |
| `accountId` | `string` | -- | Account id for multi-account channels |
| `session` | `string` | -- | Session key (`"main"` or explicit) |
| `ackMaxChars` | `number` | `30` | Max chars after HEARTBEAT_OK before delivery |
| `includeReasoning` | `boolean` | `false` | Deliver model reasoning as separate message |

### Per-Role Patterns

| Agent Type | Frequency | Active Hours | Prompt Pattern |
|------------|-----------|-------------|----------------|
| Monitor | `"30m"` | 24/7 (no activeHours) | "Check system status, report anomalies" |
| Assistant | `"1h"` | Business hours | "Review pending tasks, surface needs" |
| Batch worker | `"4h"` | Off-peak | "Process queued items" |
| Passive | No heartbeat | n/a | Omit the heartbeat section entirely |

---

## Compaction

Compaction summarizes conversation history when context limits are reached. Configured via `agents.defaults.compaction`. Type: `AgentCompactionConfig`.

### Configuration

```json
{
  "agents": {
    "defaults": {
      "compaction": {
        "mode": "safeguard",
        "reserveTokensFloor": 4096,
        "maxHistoryShare": 0.5,
        "memoryFlush": {
          "enabled": true,
          "softThresholdTokens": 8000,
          "prompt": "Save important context before compaction.",
          "systemPrompt": "Preserve key facts from conversation history."
        }
      }
    }
  }
}
```

### Fields

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `mode` | `"default" \| "safeguard"` | `"default"` | Compaction mode |
| `reserveTokensFloor` | `number` | -- | Min reserve tokens for Pi compaction (0 disables) |
| `maxHistoryShare` | `number` | `0.5` | Max context share for history (0.1-0.9) |
| `memoryFlush.enabled` | `boolean` | `true` | Run pre-compaction memory flush |
| `memoryFlush.softThresholdTokens` | `number` | -- | Trigger flush when within N tokens of threshold |
| `memoryFlush.prompt` | `string` | -- | User prompt for memory flush turn |
| `memoryFlush.systemPrompt` | `string` | -- | System prompt for memory flush turn |

### Mode Comparison

| Mode | Behavior |
|------|----------|
| `"default"` | Standard summarization of older messages |
| `"safeguard"` | Aggressive pruning; enforces `maxHistoryShare` cap; recommended for long-running agents |

---

## Context Pruning

Opt-in mechanism to prune stale tool results from LLM context. Operates independently of compaction. Configured via `agents.defaults.contextPruning`. Type: `AgentContextPruningConfig`.

### Configuration

```json
{
  "agents": {
    "defaults": {
      "contextPruning": {
        "mode": "cache-ttl",
        "ttl": "30m",
        "keepLastAssistants": 3,
        "softTrimRatio": 0.7,
        "hardClearRatio": 0.9,
        "minPrunableToolChars": 500,
        "tools": {
          "allow": ["exec_command", "read_file"],
          "deny": ["memory_search"]
        },
        "softTrim": {
          "maxChars": 2000,
          "headChars": 500,
          "tailChars": 500
        },
        "hardClear": {
          "enabled": true,
          "placeholder": "[content pruned]"
        }
      }
    }
  }
}
```

### Fields

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `mode` | `"off" \| "cache-ttl"` | `"off"` | Pruning mode |
| `ttl` | `string` | -- | Cache expiry (duration string, default unit: minutes) |
| `keepLastAssistants` | `number` | -- | Protect N most recent assistant turns |
| `softTrimRatio` | `number` | -- | Context usage ratio to trigger soft trim |
| `hardClearRatio` | `number` | -- | Context usage ratio to trigger hard clear |
| `minPrunableToolChars` | `number` | -- | Minimum tool result size eligible for pruning |
| `tools.allow` | `string[]` | -- | Only prune results from these tools |
| `tools.deny` | `string[]` | -- | Never prune results from these tools |
| `softTrim.maxChars` | `number` | -- | Max chars kept after soft trim |
| `softTrim.headChars` | `number` | -- | Chars kept from result start |
| `softTrim.tailChars` | `number` | -- | Chars kept from result end |
| `hardClear.enabled` | `boolean` | -- | Enable hard clear stage |
| `hardClear.placeholder` | `string` | -- | Replacement text for cleared content |

---

## Sandbox

Sandbox isolation for agent sessions. Configured via `agents.defaults.sandbox`.

### Configuration

```json
{
  "agents": {
    "defaults": {
      "sandbox": {
        "mode": "non-main",
        "workspaceAccess": "ro",
        "scope": "session",
        "sessionToolsVisibility": "spawned",
        "docker": {
          "image": "openclaw-sandbox:latest"
        }
      }
    }
  }
}
```

### Fields

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `mode` | `"off" \| "non-main" \| "all"` | `"off"` | Sandboxing scope |
| `workspaceAccess` | `"none" \| "ro" \| "rw"` | -- | Agent workspace mount mode |
| `scope` | `"session" \| "agent" \| "shared"` | -- | Container/workspace isolation scope |
| `sessionToolsVisibility` | `"spawned" \| "all"` | `"spawned"` | Session tools targeting scope |
| `workspaceRoot` | `string` | -- | Root directory for sandbox workspaces |
| `docker` | `SandboxDockerSettings` | -- | Docker-specific settings (image, etc.) |
| `browser` | `SandboxBrowserSettings` | -- | Sandboxed browser settings |
| `prune` | `SandboxPruneSettings` | -- | Auto-prune sandbox containers |

### Production Recommendations

| Scenario | mode | workspaceAccess | scope |
|----------|------|-----------------|-------|
| Untrusted users, high security | `"all"` | `"none"` | `"session"` |
| Development assistant | `"non-main"` | `"ro"` | `"session"` |
| Read-write coding agent | `"non-main"` | `"rw"` | `"agent"` |
| Simple chatbot, no tools | `"off"` | -- | -- |

---

## Subagents

Configuration for spawned sub-agents. Set via `agents.defaults.subagents`.

### Configuration

```json
{
  "agents": {
    "defaults": {
      "subagents": {
        "maxConcurrent": 1,
        "archiveAfterMinutes": 60,
        "model": {
          "primary": "anthropic/claude-haiku-4-20250514",
          "fallbacks": ["openai/gpt-4o-mini"]
        },
        "thinking": "off"
      }
    }
  }
}
```

### Fields

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `maxConcurrent` | `number` | `1` | Max concurrent sub-agent runs (global lane) |
| `archiveAfterMinutes` | `number` | `60` | Auto-archive sub-agent sessions after N minutes |
| `model` | `string \| { primary, fallbacks }` | -- | Default model for spawned sub-agents |
| `thinking` | `string` | -- | Default thinking level (`"off"`, `"low"`, `"medium"`, `"high"`) |

Sub-agent tool policies can be restricted globally via `tools.subagents`:

```json
{
  "tools": {
    "subagents": {
      "model": "anthropic/claude-haiku-4-20250514",
      "tools": {
        "allow": ["read_file", "web_search"],
        "deny": ["exec_command", "write_file"]
      }
    }
  }
}
```

---

## Self-Correction

Self-correction is **directive-based, not configuration-based**. There is no `selfCorrection` block in `openclaw.json`.

### How It Works

Self-correction behavior is defined through prompt engineering in workspace artifact files:

| Artifact | Purpose |
|----------|---------|
| `AGENTS.md` | Operational rules including error-handling protocols, correction procedures |
| `SOUL.md` | Pre-response behavioral checks (tone, scope, factuality) |
| `memory/YYYY-MM-DD.md` | Daily append-only error and correction journal |
| `MEMORY.md` | Long-term curated learnings distilled from daily notes |

### Implementation

Add a `## Self-Correction Protocol` section to each agent's `AGENTS.md`:

```markdown
## Self-Correction Protocol

- When a tool fails, log the error and context to today's daily note
- When a user corrects you, acknowledge it, log it, and apply it
- At session start, review recent daily notes for recurring patterns
- Periodically distill recurring learnings into MEMORY.md
- Do not fabricate; when uncertain, say so
```

See `self-correction-config-reference.md` for detailed guidance on writing effective directives.

---

## Boundaries

Boundaries combine soft directives (prompt-based) and hard enforcement (runtime config).

### Soft Boundaries

Defined in `SOUL.md ## Boundaries` and `AGENTS.md ## Safety`. These are behavioral directives enforced by model instruction-following.

### Hard Boundaries (Runtime Config)

| Config Path | Type | Description |
|-------------|------|-------------|
| `channels.*.dmPolicy` | `"pairing" \| "allowlist" \| "open" \| "disabled"` | DM access control |
| `channels.*.allowFrom` | `string[]` | Sender allowlist |
| `channels.*.groupPolicy` | `"open" \| "disabled" \| "allowlist"` | Group message policy |
| `sandbox.mode` | `"off" \| "non-main" \| "all"` | Sandbox isolation |
| `sandbox.workspaceAccess` | `"none" \| "ro" \| "rw"` | Filesystem access |
| `tools.exec.security` | `"deny" \| "allowlist" \| "full"` | Shell execution control |
| `tools.profile` | `"minimal" \| "coding" \| "messaging" \| "full"` | Base tool allowlist |
| `tools.deny` | `string[]` | Hard tool denials |
| `messages.groupChat.mentionPatterns` | `string[]` | Group mention gating |
| `tools.elevated.enabled` | `boolean` | Elevated permission toggle |
| `tools.elevated.allowFrom` | `Record<string, string[]>` | Per-provider elevated sender allowlists |

### Production Checklist

- [ ] Set `channels.*.dmPolicy` to `"pairing"` or `"allowlist"` for public channels
- [ ] Set `tools.exec.security` to `"deny"` unless shell access is needed
- [ ] Set `sandbox.mode` to `"non-main"` or `"all"` for untrusted environments
- [ ] Set `sandbox.workspaceAccess` to `"ro"` or `"none"` for read-only agents
- [ ] Review `tools.deny` to block any tools the agent should never use
- [ ] Add `SOUL.md ## Boundaries` for soft behavioral guidance
- [ ] Add `AGENTS.md ## Safety` for operational safety rules

---

## Additional Agent Defaults

Other fields on `agents.defaults` relevant to hardening:

| Field | Type | Description |
|-------|------|-------------|
| `contextTokens` | `number` | Context window cap for runtime estimates |
| `thinkingDefault` | `"off" \| "minimal" \| "low" \| "medium" \| "high" \| "xhigh"` | Default thinking level |
| `verboseDefault` | `"off" \| "on" \| "full"` | Default verbose level |
| `elevatedDefault` | `"off" \| "on" \| "ask" \| "full"` | Default elevated level |
| `maxConcurrent` | `number` | Max concurrent agent runs across conversations (default: 1) |
| `skipBootstrap` | `boolean` | Skip BOOTSTRAP.md creation for pre-configured deployments |
| `bootstrapMaxChars` | `number` | Max chars for injected bootstrap files (default: 20000) |
| `mediaMaxMb` | `number` | Max inbound media size in MB |
| `blockStreamingDefault` | `"off" \| "on"` | Default block streaming level |
| `blockStreamingBreak` | `"text_end" \| "message_end"` | Block streaming boundary |
