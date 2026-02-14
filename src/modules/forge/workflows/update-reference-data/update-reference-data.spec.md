# Workflow Specification: update-reference-data

**Module:** forge
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-13

---

## Workflow Overview

**Goal:** Refresh the agentic patterns library and OpenClaw config reference against the current OpenClaw source

**Description:** Scans the OpenClaw source code to extract current configuration schema, available features, and platform capabilities. Updates The Forge's reference data so that generated configs are always valid against the latest OpenClaw version.

**Workflow Type:** Maintenance / Data Refresh

---

## Workflow Structure

### Entry Point

```yaml
---
name: update-reference-data
description: Refresh pattern library and config reference against OpenClaw source
web_bundle: true
installed_path: '{project-root}/_bmad/forge/workflows/update-reference-data'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Locate OpenClaw source | Find and validate the OpenClaw source tree |
| 02 | Extract config schema | Parse openclaw.json schema, bindings, model config |
| 03 | Extract platform features | Identify available hooks, spawn config, memory backends |
| 04 | Update pattern library | Refresh agentic pattern implementations with current features |
| 05 | Update config reference | Write updated config reference data |
| 06 | Validate references | Cross-check updated data for accuracy |

---

## Workflow Inputs

### Required Inputs

- Path to OpenClaw source code
- Current pattern library files
- Current config reference files

### Optional Inputs

- Specific sections to update (partial refresh)

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- `data/patterns/` — Updated agentic pattern library
- `data/config-reference/` — Updated OpenClaw config schema reference

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
- OpenClaw source code structure documentation

---

_Spec created on 2026-02-13 via BMAD Module workflow_
