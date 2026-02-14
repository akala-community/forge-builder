# Workflow Specification: design-orchestration

**Module:** ocf
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-11

---

## Workflow Overview

**Goal:** Design multi-agent communication patterns for an OpenClaw agent system.

**Description:** Focused workflow for designing spawn/send relationships, session routing, channel bindings, handoff protocols, failure handling, loop prevention, and subagent tool restrictions.

**Workflow Type:** Feature

---

## Workflow Structure

### Entry Point

```yaml
---
name: design-orchestration
description: Design multi-agent communication and orchestration patterns
web_bundle: true
installed_path: '{project-root}/_bmad/ocf/workflows/design-orchestration'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Agent Map | Map all agents and their relationships |
| 02 | Communication Design | Define spawn/send patterns and session routing |
| 03 | Channel Bindings | Configure channel-to-agent routing |
| 04 | Failure Handling | Design handoff failure patterns and loop prevention |
| 05 | Subagent Policies | Define tool restrictions for spawned subagents |

---

## Workflow Inputs

### Required Inputs

- Agent roster with roles and responsibilities
- Channel requirements

### Optional Inputs

- Existing orchestration patterns to extend

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- Orchestration design document with routing tables, handoff patterns, and failure handling specs

---

## Agent Integration

### Primary Agent

Vulcan (Forge Master) — orchestration architecture is a Forge Master concern

### Other Agents

Cog (Gear Wright) — translates orchestration design into configuration

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

---

_Spec created on 2026-02-11 via BMAD Module workflow_
