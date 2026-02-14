# Agents Reference

forge includes 2 specialized agents:

---

## The Forge — Agentic System Architect

**ID:** `_bmad/forge/agents/forge.md`
**Icon:** anvil

**Role:**
Agentic System Architect — designs, builds, configures, and deploys multi-agent systems on OpenClaw. Takes natural language descriptions and produces production-ready, hardened agent deployments using Anthropic's proven agentic patterns.

**When to Use:**
Use The Forge when you want to create, extend, or harden a multi-agent system on OpenClaw. It handles the full lifecycle from design to deployment.

**Key Capabilities:**
- Full multi-agent architecture design and deployment (design-system)
- Add agents to existing systems (add-agent)
- Agentic pattern recommendation (recommend-pattern)
- Tiered memory and knowledge graph setup (setup-knowledge)
- Long-running agent harness pattern (setup-harness)
- Production hardening (harden-workspace)
- Cross-artifact validation (validate-workspace)
- Workspace packaging and import (export-package, import-package)

**Menu Triggers:**
| Trigger | Command | Description |
|---------|---------|-------------|
| DS | design-system | Full multi-agent architecture |
| AA | add-agent | Add one agent to existing system |
| RP | recommend-pattern | Match use case to agentic pattern |
| SK | setup-knowledge | Tiered memory architecture |
| SH | setup-harness | Long-running agent harness |
| HW | harden-workspace | Production hardening |
| VW | validate-workspace | Cross-artifact validation |
| EP | export-package | Bundle workspace (.ocf.zip) |
| IP | import-package | Install workspace package |

---

## Morgan — Module Lifecycle Manager

**ID:** `_bmad/forge/agents/forge-builder.md`
**Icon:** hammer

**Role:**
Module Lifecycle Manager — builds, updates, packages, and validates The Forge module itself. Morgan is the design-time agent that maintains The Forge's BMAD module lifecycle.

**When to Use:**
Use Morgan when you need to build or update The Forge's internal components — workspace files, skills, reference data — or when packaging The Forge for distribution.

**Key Capabilities:**
- Generate The Forge's workspace files (build-forge-agent)
- Generate skill definitions and bundled resources (build-forge-skill)
- Refresh pattern library and config reference (update-reference-data)
- Package The Forge for distribution (package-forge)
- Validate module consistency (validate-forge)

**Menu Triggers:**
| Trigger | Command | Description |
|---------|---------|-------------|
| BA | build-forge-agent | Generate workspace files |
| BS | build-forge-skill | Generate a skill's SKILL.md |
| UR | update-reference-data | Refresh reference data |
| PF | package-forge | Bundle into .ocf.zip |
| VF | validate-forge | Validate consistency |
