# OpenClaw Configuration Domains Reference

Reference data for the export-config workflow. Maps workspace artifacts to openclaw.json configuration sections.

---

## Configuration Domain Map

Each domain below maps workspace artifacts to their corresponding openclaw.json structure.

### 1. Agent Entries

**Source Artifacts:**
- AGENTS.md — agent roster, directives, roles
- SOUL.md — per-agent persona and identity
- agent.yaml files — agent definitions (if present)

**openclaw.json Structure:**
```json
"agents": {
  "defaults": {
    "model": "provider/model-id"
  },
  "list": [
    {
      "id": "agent-id",
      "name": "Agent Display Name",
      "workspace": "/path/to/workspace",
      "model": "provider/model-id",
      "identity": {
        "name": "Agent Name",
        "emoji": "emoji",
        "theme": "theme-name"
      }
    }
  ]
}
```

**Extraction Notes:**
- Agent ID derived from folder name or agent.yaml `id` field
- Name from SOUL.md identity or AGENTS.md header
- Model from agent config or workspace default
- Identity fields from SOUL.md persona section

---

### 2. Bindings

**Source Artifacts:**
- Channel configuration in agent files
- Orchestration patterns (if present)
- AGENTS.md channel mentions

**openclaw.json Structure:**
```json
"bindings": [
  {
    "agentId": "agent-id",
    "match": {
      "channel": "discord",
      "peer": {
        "kind": "group",
        "id": "channel-id"
      }
    }
  }
]
```

**Extraction Notes:**
- Each agent-to-channel mapping becomes a binding entry
- Multiple channels per agent = multiple binding entries
- Peer kind: "direct" for DMs, "group" for channels/groups

---

### 3. Tool Policies

**Source Artifacts:**
- Tool policy sections in AGENTS.md
- Per-agent tool configurations
- Subagent restrictions

**openclaw.json Structure:**
```json
"tools": {
  "profile": "minimal",
  "allow": ["tool-pattern"],
  "deny": ["tool-pattern"],
  "alsoAllow": ["tool-pattern"]
}
```

**Extraction Notes:**
- Goes into per-agent config: `agents.list[].tools`
- Profile maps to: minimal, coding, messaging, full
- Explicit allow/deny lists from agent directives
- Subagent restrictions in parent agent config

---

### 4. Memory Configuration

**Source Artifacts:**
- MEMORY.md — memory scaffold and structure
- _memory/ sidecar folders
- Memory directives in AGENTS.md

**openclaw.json Structure:**
```json
"memory": {
  "backend": "builtin",
  "autoCapture": true,
  "autoRecall": true,
  "embedding": {
    "provider": "openai",
    "model": "text-embedding-3-small"
  }
}
```

**Extraction Notes:**
- Global memory config goes at top level
- Per-agent memory overrides in `agents.list[].memorySearch`
- Backend options: builtin, lancedb, qmd, disabled
- Sidecar presence indicates agent needs memory paths

---

### 5. Model / Failover

**Source Artifacts:**
- Model assignments in agent configs
- Failover chains (if configured)
- Retry policies

**openclaw.json Structure:**
```json
"model": {
  "primary": "provider/model-id",
  "fallbacks": ["provider/fallback-1", "provider/fallback-2"]
}
```

**Extraction Notes:**
- Per-agent model config in `agents.list[].model`
- Can be string (simple) or object (with fallbacks)
- Fallback array processed sequentially on failure

---

### 6. Heartbeat

**Source Artifacts:**
- Heartbeat configuration in agent files
- HEARTBEAT.md (if present)
- Active hours and timezone settings

**openclaw.json Structure:**
```json
"heartbeat": {
  "every": "1h",
  "activeHours": {
    "start": "09:00",
    "end": "17:00",
    "timezone": "America/New_York"
  },
  "prompt": "Check in: review pending tasks"
}
```

**Extraction Notes:**
- Per-agent heartbeat in `agents.list[].heartbeat`
- Time units: ms, s, m, h
- ActiveHours optional — omit for 24/7 agents
- Prompt defines what the agent does on heartbeat

---

### 7. Logging

**Source Artifacts:**
- Logging configuration in workspace config
- Observability settings
- Redaction rules

**openclaw.json Structure:**
```json
"logging": {
  "level": "info",
  "consoleStyle": "pretty",
  "redactSensitive": "tools",
  "file": "/var/log/openclaw.log"
}
```

**Extraction Notes:**
- System-wide logging at top level
- Levels: fatal, error, warn, info, debug, trace
- consoleStyle: pretty (human) or json (machine)
- redactSensitive: "tools" redacts tool I/O containing secrets

---

## Workspace File Inventory Checklist

When loading a workspace, check for each of these files:

| File / Folder | Required | Contains |
|---------------|----------|----------|
| openclaw.json | No | Existing configuration (may not exist yet) |
| AGENTS.md | Yes | Agent roster, directives, roles |
| SOUL.md | Yes | Per-agent persona and identity |
| USER.md | No | User context templates |
| MEMORY.md | No | Memory scaffolds |
| REVIEW.md | No | Self-correction directives |
| HEARTBEAT.md | No | Heartbeat instructions |
| skills/ | No | Skill definitions |
| _memory/ | No | Sidecar memory folders |
| agent.yaml | No | Agent definitions |
| orchestration/ | No | Multi-agent communication patterns |
