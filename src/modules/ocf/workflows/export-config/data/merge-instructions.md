# Merge Instructions Reference

Per-section merge guidance for integrating exported configuration fragments into an existing openclaw.json.

---

## Section Merge Guide

### 1. agents.list

Append each agent entry to your existing `agents.list` array. If an agent with the same `id` already exists, replace it.

### 2. agents.defaults

Merge default settings. Your existing defaults take precedence unless you want to override them.

### 3. bindings

Append each binding entry to your existing `bindings` array. Replace `[SET_ID]` placeholders with your actual channel/chat IDs.

### 4. Per-agent tools

Already embedded in each agent entry. Review the `profile`, `allow`, and `deny` arrays for each agent.

### 5. memory

If you don't have a global memory config, add this block at the top level. If you do, review and merge manually.

### 6. Per-agent model

Already embedded in each agent entry. Replace `[SET_MODEL]` placeholders with your preferred model IDs.

### 7. Per-agent heartbeat

Already embedded in each agent entry. Adjust `every` intervals and `activeHours` for your operational needs.

### 8. logging

If you don't have logging config, add this block. If you do, review and merge manually.

---

## Placeholder Reference

| Placeholder | What It Needs |
|-------------|---------------|
| `[SET_MODEL]` | A model ID (e.g., `anthropic/claude-sonnet-4-5`) |
| `[SET_ID]` | Actual channel/chat IDs from your deployment |

---

## Assembly Rules

- Agent-level configs (tools, model, heartbeat, memorySearch) go INSIDE each agent's entry in `agents.list[]`
- System-wide configs (memory, logging) go at the top level
- Bindings are a top-level array
- Preserve all placeholder markers (`[SET_*]`)
- Ensure valid JSON structure throughout

---

## Merge Preview Rules

When performing a merge preview against an existing openclaw.json:
- Append new agents to existing agents.list
- Append new bindings to existing bindings
- Merge memory, logging (new values where existing is absent)
- Preserve all existing configuration
