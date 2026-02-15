# Workspace Assessment Reference

## Workspace Files to Load

Read the workspace directory. Load and analyze:

- **openclaw.json** (or equivalent config) — if it exists
- **AGENTS.md** — agent roster and directives
- **SOUL.md** — per-agent personas (if present)
- **USER.md** — user context templates (if present)
- **MEMORY.md** — memory scaffolds (if present)
- **REVIEW.md** — self-correction directives (if present)
- **skills/** — skill definitions (if present)
- **Any agent.yaml files** — agent definitions
- **_memory/** — sidecar folders (if present)

## Per-Agent Inventory Fields

For each agent found, document:

- Agent name and role
- Has sidecar? (yes/no)
- Current memory config (if any)
- Current tool policies (if any)
- Current failover config (if any)
- Current heartbeat config (if any)
- Current self-correction directives (if any)
- Current boundary rules (if any)

## Assessment Table Format

| Domain | Status | Details |
|--------|--------|---------|
| Memory Config | ✅ Configured / ⚠️ Partial / ❌ Missing | {what exists} |
| Tool Policies | ✅ Configured / ⚠️ Partial / ❌ Missing | {what exists} |
| Failover & Resilience | ✅ Configured / ⚠️ Partial / ❌ Missing | {what exists} |
| Observability | ✅ Configured / ⚠️ Partial / ❌ Missing | {what exists} |
| Self-Correction | ✅ Configured / ⚠️ Partial / ❌ Missing | {what exists} |
| Boundary Rules | ✅ Configured / ⚠️ Partial / ❌ Missing | {what exists} |
