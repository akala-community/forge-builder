# OCF: The Forge — Agentic System Architect

Meta-agent that designs, builds, and deploys multi-agent systems on OpenClaw

From conversation to production-ready agentic architecture

---

## Overview

The Forge is a meta-agent — an AI agent that designs, builds, configures, and deploys other AI agent systems. It lives inside OpenClaw as a native agent, accessible through any channel (WhatsApp, Telegram, Discord, TUI). Users describe what they need in natural language and The Forge generates a production-ready, multi-agent deployment — complete with the right agentic pattern, memory/knowledge architecture, and operational resilience.

The module bridges two worlds: BMAD (design-time tooling for building and maintaining The Forge itself) and OpenClaw (runtime platform where The Forge operates and where the systems it creates run).

---

## Installation

```bash
bmad install forge
```

---

## Quick Start

1. Install The Forge into your OpenClaw instance
2. Open your channel and describe the system you need: "I want to build a customer support system with 3 specialists"
3. The Forge designs the architecture, selects the right agentic pattern, and generates all workspace files
4. Review the generated config and deploy

**For detailed documentation, see [docs/](docs/).**

---

## Components

### Agents

| Agent | Name | Role |
|-------|------|------|
| The Forge | The Forge | Agentic System Architect — designs, builds, configures, and deploys multi-agent systems on OpenClaw |
| Forge Builder | Morgan | Module Lifecycle Manager — builds, updates, packages, and validates The Forge module |

### Workflows

| Workflow | Purpose |
|----------|---------|
| build-forge-agent | Generate The Forge's workspace files (SOUL.md, AGENTS.md, IDENTITY.md) |
| build-forge-skill | Generate a specific skill's SKILL.md + bundled resources |
| add-forge-skill | Define a new skill for The Forge and register it in the Forge Builder pipeline |
| update-reference-data | Refresh pattern library and config reference against OpenClaw source |
| package-forge | Bundle The Forge into installable .ocf.zip |
| validate-forge | Validate The Forge module for internal consistency |

---

## Configuration

The module supports these configuration options (set during installation):

| Variable | Description | Default |
|----------|-------------|---------|
| `forge_artifacts` | Where Forge build artifacts are stored | `{output_folder}/forge-artifacts` |

Core config variables (`user_name`, `communication_language`, `document_output_language`, `output_folder`) are inherited automatically.

---

## Module Structure

```
forge/
├── module.yaml
├── README.md
├── TODO.md
├── docs/
│   ├── getting-started.md
│   ├── agents.md
│   ├── workflows.md
│   └── examples.md
├── agents/
│   ├── forge.spec.md
│   └── forge-builder.spec.md
└── workflows/
    ├── build-forge-agent/
    ├── build-forge-skill/
    ├── add-forge-skill/
    ├── update-reference-data/
    ├── package-forge/
    └── validate-forge/
```

---

## Documentation

For detailed user guides and documentation, see the **[docs/](docs/)** folder:
- [Getting Started](docs/getting-started.md)
- [Agents Reference](docs/agents.md)
- [Workflows Reference](docs/workflows.md)
- [Examples](docs/examples.md)

---

## Development Status

This module is currently in development. The following components are planned:

- [ ] Agents: 2 agents
- [ ] Workflows: 6 workflows

See TODO.md for detailed status.

---

## Author

Created via BMAD Module workflow

---

## License

Part of the BMAD framework.
