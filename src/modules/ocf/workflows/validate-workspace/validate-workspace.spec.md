# Workflow Specification: validate-workspace

**Module:** ocf
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-11

---

## Workflow Overview

**Goal:** Check a generated workspace for internal consistency across all artifacts.

**Description:** Validates that SOUL.md personalities match AGENTS.md directives, all referenced skills are present, bindings are complete, every agent has memory directives, tool policies are defined, boundaries are set, failover is configured for customer-facing agents, and self-correction directives are present.

**Workflow Type:** Utility

---

## Workflow Structure

### Entry Point

```yaml
---
name: validate-workspace
description: Validate workspace internal consistency
web_bundle: true
installed_path: '{project-root}/_bmad/ocf/workflows/validate-workspace'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Load Workspace | Load workspace and inventory all artifacts |
| 02 | Structural Checks | Verify all required files exist and are well-formed |
| 03 | Coherence Checks | Validate cross-artifact consistency (persona vs directives, skills vs references) |
| 04 | Hardening Checks | Verify memory, tool policies, boundaries, failover, self-correction |
| 05 | Report | Generate validation report with pass/fail/warning per check |

---

## Workflow Inputs

### Required Inputs

- Path to OpenClaw workspace to validate

### Optional Inputs

- Specific checks to run (skip others)

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- Validation report with pass/fail/warning status per check

---

## Agent Integration

### Primary Agent

Cog (Gear Wright) — configuration validation specialist

### Other Agents

None

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

---

_Spec created on 2026-02-11 via BMAD Module workflow_
