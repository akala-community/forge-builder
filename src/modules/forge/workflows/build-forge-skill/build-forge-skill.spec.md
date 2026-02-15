# Workflow Specification: build-forge-skill

**Module:** forge
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-13

---

## Workflow Overview

**Goal:** Generate a specific OpenClaw skill's SKILL.md and bundled reference resources

**Description:** Takes a skill name and generates its complete SKILL.md definition plus any bundled reference data the skill needs. Discovers available skills dynamically by scanning `forge.spec.md` and the `{forge_artifacts}/skills/` directory — so newly added skills from `add-forge-skill` are always included. Each skill is a self-contained capability that The Forge agent activates at runtime.

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
| 01 | Discover available skills | Scan `{forge_artifacts}/skills/` directory and `forge.spec.md` command table to build the current skill registry — includes both original and newly added skills |
| 02 | Select skill | Present the discovered skill list to the user and let them choose which skill to build |
| 03 | Load skill context | Load relevant brief sections, pattern library, config schema, and the skill's existing spec (if updating) |
| 04 | Generate SKILL.md | Create the skill definition with triggers, flow, and instructions |
| 05 | Bundle resources | Generate any reference data the skill needs at runtime |
| 06 | Validate skill | Check skill for completeness and consistency |

---

## Workflow Inputs

### Required Inputs

- Skill name (from registered skills — discovered dynamically by scanning `forge.spec.md` command table and `{forge_artifacts}/skills/` directory)
- module-brief-forge.md (module brief)
- forge.spec.md (for command table / skill registry)
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

- `{forge_artifacts}/skills/{skill-name}/SKILL.md` — Skill definition
- `{forge_artifacts}/skills/{skill-name}/data/` — Bundled reference resources (if needed)

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
