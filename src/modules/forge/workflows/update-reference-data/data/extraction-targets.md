# Extraction Targets

Reference data for what to look for in the OpenClaw source code during extraction.

---

## Config Schema Targets

### Primary Config Files

- `**/openclaw.json` — Main configuration schema
- `**/config.ts` or `**/config.js` — Config type definitions
- `**/schema.ts` or `**/schema.js` — JSON schema definitions
- `**/types.ts` — TypeScript type definitions for config

### Config Categories to Extract

1. **Model Configuration** — Provider settings, model names, parameters, token limits
2. **Hook Configuration** — Available hooks, their triggers, configuration options
3. **Memory/State Configuration** — Memory backends, state management settings
4. **Spawn/Process Configuration** — Subprocess settings, parallelization options
5. **Permission Configuration** — Allowed/denied tools, file access, network access
6. **MCP Server Configuration** — MCP server definitions, connection settings
7. **Auth/Identity Configuration** — Authentication, API keys, identity settings

---

## Platform Feature Targets

### Hook System

- Search for: hook definitions, hook registration, hook types, hook lifecycle
- Patterns: `**/hooks/**`, `hook.ts`, `hook-*.ts`, `*Hook*`

### Spawn/Subprocess System

- Search for: spawn config, subprocess management, worker patterns
- Patterns: `**/spawn/**`, `subprocess.ts`, `worker.ts`

### Memory Backends

- Search for: memory provider definitions, state storage, persistence
- Patterns: `**/memory/**`, `**/state/**`, `*Provider*`

### Permission System

- Search for: permission definitions, access control, capability checks
- Patterns: `**/permissions/**`, `**/access/**`, `permission*.ts`

### Tool System

- Search for: tool definitions, tool registry, available tools
- Patterns: `**/tools/**`, `tool-*.ts`, `*Tool*`

---

## Extraction Output Format

For each extracted item, capture:

```yaml
name: string          # Key or feature name
type: string          # Data type or feature type
description: string   # What it does
default: any          # Default value if applicable
source_file: string   # Where found in source
source_line: number   # Line number in source
category: string      # Which category it belongs to
```
