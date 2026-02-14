# Workflow Specification: build-forge-agent

**Module:** forge
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-13

---

## Workflow Overview

**Goal:** Generate The Forge's complete OpenClaw workspace files

**Description:** Produces all the workspace files needed for The Forge agent to run inside OpenClaw — SOUL.md, AGENTS.md, IDENTITY.md, and any other required workspace artifacts. Uses the module brief and agent spec as source material.

**Workflow Type:** Build / Code Generation

---

## Workflow Structure

### Entry Point

```yaml
---
name: build-forge-agent
description: Generate The Forge's workspace files (SOUL.md, AGENTS.md, IDENTITY.md, etc.)
web_bundle: true
installed_path: '{project-root}/_bmad/forge/workflows/build-forge-agent'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Load agent spec | Load forge.spec.md and module brief |
| 02 | Generate SOUL.md | Create personality, lore, and behavioral guidelines |
| 03 | Generate IDENTITY.md | Create identity card with name, role, capabilities |
| 04 | Generate AGENTS.md | Create operational instructions and tool usage |
| 05 | Generate workspace config | Create any additional workspace files needed |
| 06 | Validate outputs | Cross-check all generated files for consistency |

---

## Workflow Inputs

### Required Inputs

- forge.spec.md (agent specification)
- module-brief-forge.md (module brief)
- OpenClaw workspace file format reference

### Optional Inputs

- Existing workspace files to merge with
- Custom personality overrides

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- `SOUL.md` — Personality, lore, behavioral guidelines
- `IDENTITY.md` — Identity card
- `AGENTS.md` — Operational instructions
- Additional workspace files as needed

---

## Agent Integration

### Primary Agent

Forge Builder (Morgan)

### Other Agents

None — Morgan builds this independently

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

Inputs needed:
- Workflow name and description
- Step structure and sequence
- Input/output specifications
- Agent associations
- OpenClaw workspace file format documentation

---

_Spec created on 2026-02-13 via BMAD Module workflow_
