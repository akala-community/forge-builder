# Workflow Specification: add-forge-skill

**Module:** forge
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-14

---

## Workflow Overview

**Goal:** Define a new skill for The Forge and register it in the Forge Builder's build pipeline

**Description:** Accepts a new skill concept from the user, generates its complete SKILL.md specification and bundled resource requirements, then registers it as a build target in Morgan's (Forge Builder) pipeline. After completion, prompts the user to run `build-forge-agent` to regenerate The Forge's workspace files with the new capability wired in.

**Workflow Type:** Build / Extensibility

---

## Workflow Structure

### Entry Point

```yaml
---
name: add-forge-skill
description: Define a new skill for The Forge and register it in the Forge Builder pipeline
web_bundle: true
installed_path: '{project-root}/_bmad/forge/workflows/add-forge-skill'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Define skill concept | Gather skill name, purpose, triggers, and scope from user |
| 02 | Load module context | Load forge.spec.md, forge-builder.spec.md, existing skills list, and module brief |
| 03 | Generate skill spec | Create the skill's SKILL.md definition with triggers, flow, instructions, and bundled resource requirements |
| 04 | Register in Forge Builder | Update forge-builder.spec.md to add the new skill as a `build-forge-skill` target |
| 05 | Update module artifacts | Update module.yaml, module-help.csv, and docs/workflows.md to reflect the new skill |
| 06 | Validate consistency | Cross-check the new skill against existing skills for naming collisions, trigger conflicts, and pattern overlap |
| 07 | Prompt rebuild | Inform user that `build-forge-agent` should be run next to regenerate The Forge's workspace files with the new capability |

---

## Workflow Inputs

### Required Inputs

- Skill name and description (from user)
- forge.spec.md (The Forge agent specification)
- forge-builder.spec.md (Morgan's agent specification)
- Existing skill specs in `skills/` directory (for conflict detection)
- module-brief-forge.md (module brief)

### Optional Inputs

- Agentic patterns library (if the skill relates to a specific pattern)
- OpenClaw config schema reference (if the skill produces config)
- Example usage scenarios

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- `skills/{skill-name}/SKILL.md` — New skill specification
- Updated `forge-builder.spec.md` — New build target registered in Morgan's command table
- Updated `module-help.csv` — New skill entry
- Updated `docs/workflows.md` — Documentation for the new skill

---

## Agent Integration

### Primary Agent

Forge Builder (Morgan)

### Other Agents

None

---

## Post-Workflow Action

After this workflow completes, the user should run **build-forge-agent** to regenerate The Forge's workspace files (SOUL.md, AGENTS.md, IDENTITY.md) so the new skill is wired into The Forge's runtime capabilities.

Pipeline: **add-forge-skill** → **build-forge-skill** → **build-forge-agent**

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

Inputs needed:
- Workflow name and description
- Step structure and sequence
- Input/output specifications
- Agent associations
- Existing skill format reference (from build-forge-skill outputs)
- forge-builder.spec.md command table format

---

_Spec created on 2026-02-14 via BMAD Module Edit workflow_
