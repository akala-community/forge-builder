# Workflow Specification: build-forge-skill

**Module:** forge
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-13

---

## Workflow Overview

**Goal:** Generate a specific OpenClaw skill's SKILL.md and bundled reference resources

**Description:** Takes a skill name (one of the 9 OpenClaw skills The Forge provides) and generates its complete SKILL.md definition plus any bundled reference data the skill needs. Each skill is a self-contained capability that The Forge agent activates at runtime.

**Workflow Type:** Build / Code Generation

---

## Workflow Structure

### Entry Point

```yaml
---
name: build-forge-skill
description: Generate a specific skill's SKILL.md + bundled resources
web_bundle: true
installed_path: '{project-root}/_bmad/forge/workflows/build-forge-skill'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Select skill | Choose which skill to build from the 9 available |
| 02 | Load skill context | Load relevant brief sections, pattern library, config schema |
| 03 | Generate SKILL.md | Create the skill definition with triggers, flow, and instructions |
| 04 | Bundle resources | Generate any reference data the skill needs at runtime |
| 05 | Validate skill | Check skill for completeness and consistency |

---

## Workflow Inputs

### Required Inputs

- Skill name (one of: design-system, add-agent, recommend-pattern, setup-knowledge, setup-harness, harden-workspace, validate-workspace, export-package, import-package)
- module-brief-forge.md (module brief)
- Agentic patterns library (for pattern-related skills)

### Optional Inputs

- OpenClaw config schema reference
- Existing skill files to update

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- `skills/{skill-name}/SKILL.md` — Skill definition
- `skills/{skill-name}/data/` — Bundled reference resources (if needed)

---

## Agent Integration

### Primary Agent

Forge Builder (Morgan)

### Other Agents

None

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

Inputs needed:
- Workflow name and description
- Step structure and sequence
- Input/output specifications
- Agent associations
- OpenClaw skill format documentation

---

_Spec created on 2026-02-13 via BMAD Module workflow_
