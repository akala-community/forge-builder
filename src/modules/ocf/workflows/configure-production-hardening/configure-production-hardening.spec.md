# Workflow Specification: configure-production-hardening

**Module:** ocf
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-11

---

## Workflow Overview

**Goal:** Layer production features onto a generated or existing OpenClaw workspace.

**Description:** Takes a workspace and adds memory configuration, tool policies, failover chains, heartbeat patterns, logging setup, self-correction directives, and boundary rules. Can be run standalone on workspaces not created by OCF.

**Workflow Type:** Feature

---

## Workflow Structure

### Entry Point

```yaml
---
name: configure-production-hardening
description: Add production hardening features to an OpenClaw workspace
web_bundle: true
installed_path: '{project-root}/_bmad/ocf/workflows/configure-production-hardening'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Load Workspace | Load workspace and assess current hardening level |
| 02 | Memory Config | Configure memory backends with auto-recall/capture per agent |
| 03 | Tool Policies | Define per-agent allow/deny lists based on role |
| 04 | Failover & Resilience | Configure model fallback chains and context overflow handling |
| 05 | Observability | Set up heartbeat patterns, logging config, and monitoring |
| 06 | Self-Correction | Add error journaling, pre-response checks, and feedback capture |
| 07 | Boundary Rules | Define privacy rules, escalation triggers, and data handling policies |

---

## Workflow Inputs

### Required Inputs

- Path to OpenClaw workspace (OCF-generated or existing)

### Optional Inputs

- Specific hardening features to focus on
- Environment target (development vs production)

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- Updated workspace artifacts with production hardening applied
- Hardening report documenting all configurations added

---

## Agent Integration

### Primary Agent

Cog (Gear Wright) — configuration and hardening specialist

### Other Agents

None

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

---

_Spec created on 2026-02-11 via BMAD Module workflow_
