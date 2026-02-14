# Workflow Specification: create-skill

**Module:** ocf
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-11

---

## Workflow Overview

**Goal:** Generate a complete OpenClaw skill with SKILL.md, executable scaffold, and gating rules.

**Description:** Creates a fully structured OpenClaw skill including proper frontmatter, executable code scaffold, gating rules (OS, binary requirements, env vars). Ensures security scanner compliance — no eval, no exec unless explicitly documented.

**Workflow Type:** Feature

---

## Workflow Structure

### Entry Point

```yaml
---
name: create-skill
description: Generate a complete OpenClaw skill
web_bundle: true
installed_path: '{project-root}/_bmad/ocf/workflows/create-skill'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Skill Requirements | Gather skill purpose, triggers, inputs/outputs |
| 02 | Gating Rules | Define OS, binary, and env var requirements |
| 03 | Code Scaffold | Generate executable scaffold with security compliance |
| 04 | SKILL.md Generation | Assemble complete SKILL.md with frontmatter |

---

## Workflow Inputs

### Required Inputs

- Skill name and purpose
- Target agent(s) that will use this skill

### Optional Inputs

- Specific gating requirements
- Code examples or references

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- `skills/{skill-name}/SKILL.md` — Complete skill definition
- `skills/{skill-name}/` — Executable scaffold files

---

## Agent Integration

### Primary Agent

Cog (Gear Wright) — skills and configuration specialist

### Other Agents

None

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

---

_Spec created on 2026-02-11 via BMAD Module workflow_
