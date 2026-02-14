# Workflow Specification: edit-agent-system

**Module:** ocf
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-11

---

## Workflow Overview

**Goal:** Modify an existing generated workspace while maintaining coherence across all artifacts.

**Description:** Change one agent's persona, skills, or configuration and propagate implications to memory scaffolds, tool policies, directives, and other interconnected artifacts. Ensures the system stays internally consistent after edits.

**Workflow Type:** Feature

---

## Workflow Structure

### Entry Point

```yaml
---
name: edit-agent-system
description: Edit existing agent systems with coherence maintenance
web_bundle: true
installed_path: '{project-root}/_bmad/ocf/workflows/edit-agent-system'
---
```

### Mode

- [ ] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Load Workspace | Load existing workspace and inventory all artifacts |
| 02 | Identify Changes | Determine what the user wants to modify |
| 03 | Impact Analysis | Analyze which artifacts are affected by the change |
| 04 | Apply Changes | Modify artifacts and propagate implications |
| 05 | Coherence Check | Verify internal consistency after edits |

---

## Workflow Inputs

### Required Inputs

- Path to existing generated workspace
- Description of desired changes

### Optional Inputs

- Specific artifacts to modify

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- Updated workspace artifacts (in-place modifications)
- Change report documenting what was modified and why

---

## Agent Integration

### Primary Agent

Anima (Soul Smith) — persona and identity changes; Cog (Gear Wright) — config and skill changes

### Other Agents

Vulcan (Forge Master) — consulted for architectural implications

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

---

_Spec created on 2026-02-11 via BMAD Module workflow_
