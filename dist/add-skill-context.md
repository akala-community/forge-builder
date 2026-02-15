---
skillName: 'channel-setup'
skillCategory: 'feature'
skillPurpose: 'Generate a platform-specific channel layout plan and implementation configuration for a Forge workspace, mapping each agent to a dedicated channel with proper categories, naming, and per-channel welcome/instruction content.'
stepsCompleted: ['step-01-define-concept', 'step-02-load-context', 'step-03-generate-spec', 'step-04-register-skill', 'step-05-update-artifacts', 'step-06-validate', 'step-07-complete']
status: COMPLETE
completedDate: '2026-02-14'
date: '2026-02-14'
---

# Add Skill: channel-setup

## Skill Concept

**Name:** channel-setup
**Category:** Feature
**Purpose:** Generate a platform-specific channel layout plan and implementation configuration for a Forge workspace, mapping each agent to a dedicated channel with proper categories, naming, and per-channel welcome/instruction content. Currently supports Discord as the primary channel provider.

### Triggers

- "set up channels for my workspace"
- "configure discord channels for my agents"
- "channel setup"
- "create channel plan for my agents"
- "set up discord for my forge workspace"

### Scope

**Reads:** Agent roster/definitions (AGENTS.md or equivalent), workspace architecture
**Creates/Modifies:** Channel plan document, per-channel configuration (names, categories, descriptions, welcome messages, agent invocation instructions)
**Depends on:** Agent roster and architecture must exist (runs after agent definitions are complete)
**Leads to:** Platform-specific implementation (Discord bot setup, channel creation scripts, or manual setup guide)

### Flow Overview

1. Read the workspace's agent roster and architecture to identify all agents and their roles
2. Ask user which channel provider they're using (Discord initially, extensible)
3. Generate a channel plan — propose categories, channel names, and agent-to-channel mapping
4. Present plan to user for review and iteration
5. Once confirmed, generate per-channel configuration: channel descriptions, welcome/pinned messages with agent invocation instructions (e.g., `@AgentName` on Discord)
6. Output the full channel setup document — either as a manual setup guide or automation-ready config
7. Optionally generate platform-specific automation (e.g., Discord bot script to create channels)

---

## Loaded Context

### The Forge Agent Spec

**Current Commands:**

| Trigger | Command | Description |
|---------|---------|-------------|
| DS | design-system | Full multi-agent architecture design and deployment |
| AA | add-agent | Add one agent to existing system |
| RP | recommend-pattern | Match use case to agentic pattern |
| EA | equip-agents | Research and bind concrete tools to each agent's capabilities |
| SK | setup-knowledge | Tiered memory and knowledge graph architecture |
| SH | setup-harness | Long-running agent harness pattern |
| HW | harden-workspace | Systematic production hardening |
| VW | validate-workspace | Cross-artifact validation |
| EP | export-package | Bundle workspace for sharing (.ocf.zip) |
| IP | import-package | Install workspace package |

**Communication Style:** Precise yet approachable. Forge metaphors (blueprints, tempering, quality inspection). Voice shifts by activity phase.

### Forge Builder Spec (Morgan)

**Current Build Commands:**

| Trigger | Command | Description |
|---------|---------|-------------|
| BA | build-forge-agent | Generate workspace files (SOUL.md, AGENTS.md, IDENTITY.md) |
| BS | build-forge-skill | Generate a skill's SKILL.md + bundled resources |
| AS | add-forge-skill | Define new skill and register in build pipeline |
| UR | update-reference-data | Refresh pattern library and config reference |
| PF | package-forge | Bundle into .ocf.zip |
| VF | validate-forge | Validate module consistency |

**Existing Trigger Mappings:** BA, BS, AS, UR, PF, VF (all 2-letter uppercase)

### Existing Skills

**Count:** 10 built (in `_bmad-output/forge-artifacts/skills/`)
**Skills:**

| Name | Category | Key Triggers |
|------|----------|-------------|
| design-system | Core | "build me a team", "create agents", "I need a system for..." |
| add-agent | Core | "add an agent", "I need another agent for..." |
| recommend-pattern | Core | "what pattern should I use", "how should I architect..." |
| equip-agents | Feature | "equip my agents with tools", "what tools do my agents need", "set up tools for the team" |
| setup-knowledge | Feature | "set up memory", "knowledge graph", "agents should remember..." |
| setup-harness | Feature | "long running tasks", "multi-session", "checkpoint..." |
| harden-workspace | Feature | "production ready", "harden", "secure my agents" |
| validate-workspace | Utility | "validate", "check my setup", "anything wrong?" |
| export-package | Utility | "export", "package", "share my setup" |
| import-package | Utility | "import", "install package" |

### Module Brief Extract

Not available — `forge_module_brief` not defined in config.

### Context Summary

**Key inputs for SKILL.md generation:**
- Existing commands: 10 in The Forge, 6 in Forge Builder
- Existing skills: 10 built
- Potential trigger conflicts: None detected — "channel" is unique, no existing skill uses "channel", "discord", or "channel setup" triggers
- Available trigger letter: **CS** (Channel Setup) — unused in both The Forge and Forge Builder command tables
- Pipeline insertion point: After `design-system` Phase 3 (agent roster confirmed) or after `equip-agents`. Also standalone when agent roster already exists.
- Closest existing skill: `equip-agents` (provisions tools for agents) — but that skill researches and binds *tools*, not *communication channels*. No overlap.

---

## Spec Generation Complete

**SKILL.md written to:** `_bmad/forge/skills/channel-setup/SKILL.md`
**Sections generated:** Triggers, Execution Flow, Instructions, Data Dependencies, Connected Skills, Success Criteria
**User confirmed:** Yes

---

## Registration Complete

**The Forge:**
- Trigger: CS
- Command: channel-setup
- Added to command table: Yes (positioned after equip-agents)

**Forge Builder (Morgan):**
- Added to command table: No — channel-setup is a runtime Forge skill, not a build command. Discoverable by existing BS (build-forge-skill) command via skills directory.

---

## Module Artifacts Updated

**module-help.csv:** Entry added for channel-setup
**docs/workflows.md:** Section added for channel-setup, count updated from 6 to 7

---

## Validation Report

**Date:** 2026-02-14
**Skill:** channel-setup
**Result:** 6/6 checks passed
**Status:** VALIDATED

### Check Results

1. Structural Completeness — PASS (all 7 required sections present)
2. Naming Collision — PASS (unique name, kebab-case, no BMAD conflicts)
3. Trigger Conflict — PASS (CS unique, trigger phrases unique, primary + contextual defined)
4. Registration Integrity — PASS (forge.spec.md updated, entry matches SKILL.md metadata)
5. Documentation Completeness — PASS (module-help.csv + docs/workflows.md updated, count accurate)
6. Connected Skills Consistency — PASS (all referenced skills exist, no circular dependencies)

### Issues Found

None

### Fixes Applied

None requested
