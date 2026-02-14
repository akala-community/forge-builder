# Workflow Specification: create-single-agent

**Module:** ocf
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-11

---

## Workflow Overview

**Goal:** Streamlined workflow for creating a single agent workspace (brief + generation in one flow).

**Description:** Combines the brief and generation phases into a single streamlined flow for users who need just one agent. Produces a complete single-agent workspace with all artifacts.

**Workflow Type:** Core

---

## Workflow Structure

### Entry Point

```yaml
---
name: create-single-agent
description: Streamlined single agent workspace creation
web_bundle: true
installed_path: '{project-root}/_bmad/ocf/workflows/create-single-agent'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Quick Brief | Gather agent concept, persona, skills, and channel needs in one pass |
| 02 | Identity & Config | Generate SOUL.md, AGENTS.md, USER.md, MEMORY.md, skills, and config |
| 03 | Assembly | Assemble single-agent workspace and present for review |

---

## Workflow Inputs

### Required Inputs

- User's single agent concept (gathered through conversation)

### Optional Inputs

- Channel requirements
- Existing OpenClaw workspace to integrate with

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- `{ocf_output_folder}/{agent-name}/` — Complete single-agent workspace

---

## Agent Integration

### Primary Agent

Anima (Soul Smith) — handles the streamlined flow

### Other Agents

None — single-agent flow doesn't require full pipeline

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

---

_Spec created on 2026-02-11 via BMAD Module workflow_
