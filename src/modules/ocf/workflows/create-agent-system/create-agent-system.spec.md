# Workflow Specification: create-agent-system

**Module:** ocf
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-11

---

## Workflow Overview

**Goal:** Take a structured brief and generate the complete OpenClaw workspace with all artifacts.

**Description:** Generates AGENTS.md, SOUL.md, USER.md, MEMORY.md scaffolds, skills directory, REVIEW.md, openclaw.json configuration fragments, and workspace directory structure for every agent in the system.

**Workflow Type:** Core

---

## Workflow Structure

### Entry Point

```yaml
---
name: create-agent-system
description: Generate complete OpenClaw workspace from a brief
web_bundle: true
installed_path: '{project-root}/_bmad/ocf/workflows/create-agent-system'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Load Brief | Load and validate the agent system brief |
| 02 | Identity Generation | Generate SOUL.md and AGENTS.md for each agent (Anima phase) |
| 03 | Context Generation | Generate USER.md templates and MEMORY.md scaffolds per agent |
| 04 | Skill Generation | Generate skills directory with SKILL.md files per agent |
| 05 | Config Generation | Generate openclaw.json fragments, tool policies, memory config, failover, heartbeat, logging |
| 06 | Self-Correction | Generate REVIEW.md and self-correction directives per agent |
| 07 | Assembly | Assemble complete workspace directory structure |
| 08 | Review | Present generated workspace for user review and refinement |

---

## Workflow Inputs

### Required Inputs

- Structured agent system brief (from create-agent-brief workflow)

### Optional Inputs

- Existing OpenClaw configuration for reference
- Custom templates or overrides

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- `{ocf_output_folder}/{system-name}/` — Complete workspace directory containing:
  - Per-agent: AGENTS.md, SOUL.md, USER.md, MEMORY.md, skills/, REVIEW.md
  - System-level: openclaw.json fragments, tool policies, memory config, failover config, heartbeat config, logging config

---

## Agent Integration

### Primary Agent

Anima (Soul Smith) — leads identity generation; Cog (Gear Wright) — leads config and assembly

### Other Agents

Vulcan (Forge Master) — provides architecture context from the brief

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

---

_Spec created on 2026-02-11 via BMAD Module workflow_
