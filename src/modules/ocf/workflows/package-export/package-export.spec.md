# Workflow Specification: package-export

**Module:** ocf
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-11

---

## Workflow Overview

**Goal:** Bundle a completed workspace into a portable .zip archive + companion setup prompt.

**Description:** Takes a completed workspace and packages it into `{agent-system-name}.ocf.zip` containing all workspace files plus `{agent-system-name}.setup.md` with step-by-step instructions for an OpenClaw agent to unpack and activate the system. Includes OCF metadata for upgrade-path tracking.

**Workflow Type:** Utility

---

## Workflow Structure

### Entry Point

```yaml
---
name: package-export
description: Bundle workspace into portable zip + setup prompt
web_bundle: true
installed_path: '{project-root}/_bmad/ocf/workflows/package-export'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Load Workspace | Load and validate workspace completeness |
| 02 | Metadata Injection | Add OCF version and template metadata to artifacts |
| 03 | Setup Prompt Generation | Generate setup.md with installation instructions |
| 04 | Package Assembly | Bundle workspace + setup prompt into .ocf.zip |

---

## Workflow Inputs

### Required Inputs

- Path to completed workspace

### Optional Inputs

- Custom setup instructions
- Target OpenClaw version

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- `{ocf_output_folder}/packages/{system-name}.ocf.zip` — Portable workspace archive
- `{ocf_output_folder}/packages/{system-name}.setup.md` — Companion setup prompt

---

## Agent Integration

### Primary Agent

Cog (Gear Wright) — assembly and packaging specialist

### Other Agents

None

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

---

_Spec created on 2026-02-11 via BMAD Module workflow_
