# Workflow Specification: package-import

**Module:** ocf
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-11

---

## Workflow Overview

**Goal:** Receive an .ocf.zip + setup prompt and execute the installation on a running OpenClaw instance.

**Description:** The reverse flow of package-export. An OpenClaw agent receives an .ocf.zip + setup prompt via any channel and executes the installation: extracts workspace files to the correct directories, merges openclaw.json configuration, registers agent entries, sets up bindings, and activates the new agent system.

**Workflow Type:** Utility

---

## Workflow Structure

### Entry Point

```yaml
---
name: package-import
description: Receive and install an OCF package
web_bundle: true
installed_path: '{project-root}/_bmad/ocf/workflows/package-import'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Receive Package | Accept and validate the .ocf.zip archive |
| 02 | Extract | Unpack workspace files to target directories |
| 03 | Configure | Merge openclaw.json fragments into existing configuration |
| 04 | Register | Register agent entries and set up bindings |
| 05 | Activate | Bring the new agent system online and verify |

---

## Workflow Inputs

### Required Inputs

- .ocf.zip archive
- setup.md prompt (companion to the archive)

### Optional Inputs

- Target installation directory
- Configuration overrides

---

## Workflow Outputs

### Output Format

- [ ] Document-producing
- [x] Non-document

### Output Files

- Installed workspace files in target directories
- Merged openclaw.json configuration
- Installation report

---

## Agent Integration

### Primary Agent

Cog (Gear Wright) — assembly and installation specialist

### Other Agents

None

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

---

_Spec created on 2026-02-11 via BMAD Module workflow_
