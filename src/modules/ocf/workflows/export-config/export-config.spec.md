# Workflow Specification: export-config

**Module:** ocf
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-11

---

## Workflow Overview

**Goal:** Extract and format openclaw.json fragments ready for merge into an existing OpenClaw installation.

**Description:** Reads a generated workspace and extracts all openclaw.json configuration fragments — agent entries, bindings, tool policies, memory backends, failover, heartbeat, logging — formatted for direct merge into an existing openclaw.json.

**Workflow Type:** Utility

---

## Workflow Structure

### Entry Point

```yaml
---
name: export-config
description: Extract openclaw.json fragments for merge
web_bundle: true
installed_path: '{project-root}/_bmad/ocf/workflows/export-config'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Load Workspace | Load workspace and identify all configuration artifacts |
| 02 | Extract Fragments | Collect all openclaw.json-relevant configuration |
| 03 | Format Output | Format fragments for merge with clear section markers |

---

## Workflow Inputs

### Required Inputs

- Path to generated workspace

### Optional Inputs

- Existing openclaw.json to preview merge result

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- `openclaw-config-{system-name}.json` — Formatted configuration fragments

---

## Agent Integration

### Primary Agent

Cog (Gear Wright) — configuration specialist

### Other Agents

None

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

---

_Spec created on 2026-02-11 via BMAD Module workflow_
