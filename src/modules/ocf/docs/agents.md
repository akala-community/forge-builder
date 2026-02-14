# Agents Reference

OCF includes 3 specialized agents forming the forge team:

---

## Forge Master — Vulcan

**ID:** `_bmad/ocf/agents/forge-master.md`
**Icon:** 🔥

**Role:**
Lead Architect & Brief Creator. Handles the brief and architecture phase -- gathering requirements, designing the agent roster, planning orchestration patterns, memory architecture, resilience strategy, and observability needs.

**When to Use:**
Start here when you have a new agent system idea. Vulcan is the entry point for all multi-agent system creation. Also use Vulcan when you need to design or redesign orchestration patterns for an existing system.

**Key Capabilities:**
- Guided requirements gathering for agent systems
- Agent roster design and role definition
- Multi-agent orchestration architecture
- Memory architecture planning
- Resilience and observability strategy

**Menu Triggers:**
- `[AB]` Create Agent Brief
- `[DO]` Design Orchestration

---

## Soul Smith — Anima

**ID:** `_bmad/ocf/agents/soul-smith.md`
**Icon:** ✨

**Role:**
Persona & Identity Designer. Takes the architecture from Vulcan and crafts each agent's identity -- SOUL.md personas, AGENTS.md directives, USER.md context, self-correction patterns, boundary rules, and feedback capture patterns.

**When to Use:**
After Vulcan has completed the brief and architecture. Anima handles the "soul" of each agent. Also use Anima for the streamlined single-agent flow or when editing existing agent identities.

**Key Capabilities:**
- SOUL.md persona creation with coherent personality
- AGENTS.md directive generation with self-correction patterns
- USER.md context templates
- Boundary and safety rule design
- Feedback capture pattern design

**Menu Triggers:**
- `[CS]` Create Agent System
- `[SA]` Create Single Agent
- `[EA]` Edit Agent System

---

## Gear Wright — Cog

**ID:** `_bmad/ocf/agents/gear-wright.md`
**Icon:** ⚙️

**Role:**
Skills, Config & Assembly Engineer. Takes the identities and architecture, then generates skills, configuration, tool policies, memory scaffolds, resilience config, and assembles the final workspace. Handles packaging and deployment flows.

**When to Use:**
After Anima has completed identity design. Cog handles everything technical -- skills, configuration, assembly, validation, and packaging. Also use Cog standalone for production hardening, workspace validation, or package export/import.

**Key Capabilities:**
- SKILL.md generation with security compliance
- openclaw.json configuration fragments
- Tool policy and memory backend configuration
- Failover, heartbeat, and logging setup
- Workspace assembly and directory structuring
- Portable package creation (zip + setup prompt)
- Package import and self-installation

**Menu Triggers:**
- `[SK]` Create Skill
- `[PH]` Production Hardening
- `[VW]` Validate Workspace
- `[EC]` Export Config
- `[PE]` Package Export
- `[PI]` Package Import
