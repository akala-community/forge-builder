# Workflow Specification: create-agent-brief

**Module:** ocf
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-11

---

## Workflow Overview

**Goal:** Guide users through structured discovery of a new OpenClaw agent system (single or multi-agent).

**Description:** Guided discovery producing a structured brief covering all aspects: agents, personas, skills, channels, orchestration, memory architecture, resilience needs, and safety requirements.

**Workflow Type:** Core

---

## Workflow Structure

### Entry Point

```yaml
---
name: create-agent-brief
description: Guided discovery of a new OpenClaw agent system
web_bundle: true
installed_path: '{project-root}/_bmad/ocf/workflows/create-agent-brief'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Concept Gathering | Capture the user's agent system idea and high-level goals |
| 02 | Agent Roster Design | Define agents, their roles, personas, and responsibilities |
| 03 | Skill & Channel Mapping | Identify skills, tools, and channel bindings per agent |
| 04 | Orchestration Planning | Design multi-agent communication, routing, and handoff patterns |
| 05 | Memory & Resilience | Plan memory architecture, self-correction, failover, and safety |
| 06 | Brief Assembly | Compile all gathered information into the structured brief document |

---

## Workflow Inputs

### Required Inputs

- User's agent system concept/idea (gathered through conversation)

### Optional Inputs

- Existing OpenClaw workspace for reference
- Channel requirements (WhatsApp, Telegram, Discord, etc.)

---

## Workflow Outputs

### Output Format

- [x] Document-producing
- [ ] Non-document

### Output Files

- `{ocf_output_folder}/briefs/agent-brief-{system-name}.md` — Structured brief document

---

## Agent Integration

### Primary Agent

Vulcan (Forge Master) — leads the discovery and architecture phase

### Other Agents

None — this is the entry-point workflow before handoff

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

---

_Spec created on 2026-02-11 via BMAD Module workflow_
