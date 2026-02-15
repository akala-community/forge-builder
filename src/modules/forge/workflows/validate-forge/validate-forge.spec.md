# Workflow Specification: validate-forge

**Module:** forge
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-13

---

## Workflow Overview

**Goal:** Validate The Forge module for internal consistency

**Description:** Runs a comprehensive consistency check across all Forge artifacts — workspace files, skills, reference data, config schema. Ensures everything is aligned and nothing is missing or contradictory before packaging or deployment.

**Workflow Type:** Quality Assurance / Validation

---

## Workflow Structure

### Entry Point

```yaml
---
name: validate-forge
description: Validate The Forge module for internal consistency
web_bundle: true
installed_path: '{project-root}/_bmad/forge/workflows/validate-forge'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Load all artifacts | Collect all workspace files, skills, and reference data |
| 02 | Structural checks | Verify all required files exist and have correct format |
| 03 | Coherence checks | Cross-reference skills against patterns library, config schema |
| 04 | Completeness checks | Ensure all registered skills (discovered from `forge.spec.md` and `{forge_artifacts}/skills/`) are present with required resources |
| 05 | Generate report | Produce validation report with pass/fail/warnings |

---

## Workflow Inputs

### Required Inputs

- All generated workspace files
- All generated skill files
- Reference data files
- module-brief-forge.md (source of truth for completeness)

### Optional Inputs

- Previous validation report (for delta comparison)

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- `{forge_artifacts}/validation-report.md` — Full validation report with findings

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
- Validation criteria derived from module brief

---

_Spec created on 2026-02-13 via BMAD Module workflow_
