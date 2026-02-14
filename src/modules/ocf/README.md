# OpenClaw Forge (OCF)

End-to-end agent factory for OpenClaw

Forge complete, production-hardened multi-agent workspaces from concept to deployment

---

## Overview

The OpenClaw Forge is a BMAD-powered module that serves as an end-to-end agent factory for the OpenClaw platform. It takes users from initial concept -- "I want an agent that does X" -- through to a fully deployable, production-hardened multi-agent workspace complete with all artifacts: AGENTS.md, SOUL.md, USER.md, MEMORY.md, skills, openclaw.json configuration fragments, orchestration patterns, guardrails, and resilience configuration.

OCF eliminates the friction of manually constructing OpenClaw workspaces by providing guided workflows that understand OpenClaw's architecture deeply and generate coherent, interconnected agent systems that work together out of the box.

---

## Installation

```bash
bmad install ocf
```

---

## Quick Start

1. Activate the **Forge Master (Vulcan)** agent
2. Use the **Create Agent Brief** command to describe your agent system idea
3. Walk through the guided discovery -- Vulcan will help you design the architecture
4. The brief passes to **Soul Smith (Anima)** for persona and identity design
5. Then to **Gear Wright (Cog)** for skills, configuration, and final assembly
6. Review your complete workspace and package it for deployment

**For detailed documentation, see [docs/](docs/).**

---

## Components

### Agents

| Agent | Name | Role |
|-------|------|------|
| Forge Master | Vulcan | Lead Architect & Brief Creator |
| Soul Smith | Anima | Persona & Identity Designer |
| Gear Wright | Cog | Skills, Config & Assembly Engineer |

### Workflows

**Core:**
- **create-agent-brief** — Guided discovery of a new OpenClaw agent system
- **create-agent-system** — Generate complete workspace from a brief
- **create-single-agent** — Streamlined single agent creation

**Feature:**
- **design-orchestration** — Design multi-agent communication patterns
- **create-skill** — Generate complete OpenClaw skills
- **edit-agent-system** — Modify existing workspaces with coherence
- **configure-production-hardening** — Layer production features onto workspaces

**Utility:**
- **validate-workspace** — Check workspace internal consistency
- **export-config** — Extract openclaw.json fragments
- **package-export** — Bundle workspace into portable zip + setup prompt
- **package-import** — Receive and install OCF packages

---

## Configuration

The module supports these configuration options (set during installation):

| Variable | Description | Default |
|----------|-------------|---------|
| `ocf_output_folder` | Where generated OpenClaw workspaces are saved | `{output_folder}/ocf-workspaces` |

Core config variables (`user_name`, `communication_language`, `document_output_language`, `output_folder`) are also available automatically.

---

## Module Structure

```
ocf/
├── module.yaml
├── README.md
├── TODO.md
├── docs/
│   ├── getting-started.md
│   ├── agents.md
│   ├── workflows.md
│   └── examples.md
├── agents/
│   ├── forge-master.spec.md
│   ├── soul-smith.spec.md
│   └── gear-wright.spec.md
└── workflows/
    ├── create-agent-brief/
    ├── create-agent-system/
    ├── create-single-agent/
    ├── design-orchestration/
    ├── create-skill/
    ├── edit-agent-system/
    ├── configure-production-hardening/
    ├── validate-workspace/
    ├── export-config/
    ├── package-export/
    └── package-import/
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

- [ ] Agents: 3 agents
- [ ] Workflows: 11 workflows

See TODO.md for detailed status.

---

## Author

Created via BMAD Module workflow

---

## License

Part of the BMAD framework.
