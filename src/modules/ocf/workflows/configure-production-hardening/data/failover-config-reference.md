# Failover Configuration Reference

## Model Failover

Model redundancy is configured per-agent via `agents.defaults.model` (and optionally `agents.defaults.imageModel`). The runtime attempts the primary model first; on failure (API error, rate limit, timeout), it cascades through the `fallbacks` array sequentially.

Failover logic lives in `src/agents/model-fallback.ts`. It uses auth profile rotation (`src/agents/auth-profiles.ts`) to skip providers whose profiles are all in cooldown, then tries each remaining candidate in order.

### Configuration (openclaw.json)

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
      "timeoutSeconds": 30
    }
  }
}
```

### TypeScript Types (from `src/config/types.agent-defaults.ts`)

```typescript
type AgentModelListConfig = {
  primary?: string;     // "provider/model" format
  fallbacks?: string[]; // tried in order on primary failure
};
```

Both `model` and `imageModel` use the same `AgentModelListConfig` shape.

### Model Aliases

The `models` record in `agents.defaults` supports aliases and per-model parameters:

```json
{
  "agents": {
    "defaults": {
      "models": {
        "anthropic/claude-sonnet-4-20250514": {
          "alias": "sonnet",
          "streaming": true
        },
        "ollama/llama3": {
          "alias": "local",
          "streaming": false
        }
      }
    }
  }
}
```

Aliases can be used in `model.primary` and `model.fallbacks` fields.

### Timeout

The `timeoutSeconds` field sets the per-request timeout. This is a flat integer on `agents.defaults`:

```json
{
  "agents": {
    "defaults": {
      "timeoutSeconds": 30
    }
  }
}
```

### Recommended Fallback Chains

**Complex tasks (primary agents):**
1. `anthropic/claude-sonnet-4-20250514`
2. `openai/gpt-4o`
3. `anthropic/claude-haiku-4-20250514`

**Lightweight tasks (subagents):**
1. `anthropic/claude-haiku-4-20250514`
2. `openai/gpt-4o-mini`

**Local-first setups:**
1. `ollama/llama3`
2. `anthropic/claude-haiku-4-20250514`

---

## Retry Policy

Retry logic is **not user-configurable** in `openclaw.json`. It is hardcoded at the engine level.

- **Model failover** is handled by `src/agents/model-fallback.ts` using auth profile rotation. When a model fails, the system tries the next fallback. When all auth profiles for a provider are in cooldown, that provider is skipped entirely.
- **Channel-specific retries** exist only for Discord and Telegram delivery, with hardcoded defaults in `src/infra/retry-policy.ts`:

| Channel | Attempts | Min Delay | Max Delay | Jitter |
|---------|----------|-----------|-----------|--------|
| Discord | 3 | 500ms | 30s | 0.1 |
| Telegram | 3 | 400ms | 30s | 0.1 |

Discord retries on `RateLimitError`. Telegram retries on 429, timeout, connection reset, and similar transient errors, and respects `retry_after` headers from the Telegram API.

There is no user-facing retry configuration block. To improve resilience, add more entries to `model.fallbacks`.

---

## Compaction

When the context window fills up, the compaction system summarizes conversation history. This is configured via `agents.defaults.compaction`.

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
          "prompt": "Save important context to memory before compaction.",
          "systemPrompt": "You are about to lose conversation history. Preserve key facts."
        }
      }
    }
  }
}
```

### TypeScript Types

```typescript
type AgentCompactionConfig = {
  mode?: "default" | "safeguard";
  reserveTokensFloor?: number;         // min reserve tokens (0 disables)
  maxHistoryShare?: number;             // 0.1-0.9, default 0.5
  memoryFlush?: {
    enabled?: boolean;                  // default: true
    softThresholdTokens?: number;       // run flush when within N tokens of threshold
    prompt?: string;                    // user prompt for the flush turn
    systemPrompt?: string;             // system prompt appended for flush turn
  };
};
```

### Modes

| Mode | Behavior |
|------|----------|
| `default` | Standard compaction summarization |
| `safeguard` | More aggressive pruning; enforces `maxHistoryShare` cap on history |

---

## Context Pruning

Context pruning is a separate, opt-in mechanism that removes stale tool results from the LLM context to reduce token usage. It operates independently of compaction.

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

### TypeScript Types

```typescript
type AgentContextPruningConfig = {
  mode?: "off" | "cache-ttl";
  ttl?: string;                        // duration string (default unit: minutes)
  keepLastAssistants?: number;
  softTrimRatio?: number;
  hardClearRatio?: number;
  minPrunableToolChars?: number;
  tools?: {
    allow?: string[];                   // only prune these tool results
    deny?: string[];                    // never prune these tool results
  };
  softTrim?: {
    maxChars?: number;                  // max chars to keep after soft trim
    headChars?: number;                 // chars to keep from start
    tailChars?: number;                 // chars to keep from end
  };
  hardClear?: {
    enabled?: boolean;
    placeholder?: string;              // replacement text for cleared content
  };
};
```

### Pruning Stages

| Stage | Trigger | Action |
|-------|---------|--------|
| Soft trim | `softTrimRatio` of context used | Truncate large tool results to `headChars + tailChars` |
| Hard clear | `hardClearRatio` of context used | Replace prunable tool results with placeholder text |

The `tools.allow` / `tools.deny` lists control which tool results are eligible for pruning. The `keepLastAssistants` value protects the N most recent assistant turns from pruning.
