---
conversionFrom: 'src/modules/ocf/workflows/design-orchestration/design-orchestration.spec.md'
originalFormat: 'BMAD Workflow Specification (placeholder spec)'
workflowName: design-orchestration
creationDate: 2026-02-11
completionDate: 2026-02-11
status: COMPLETE
confirmationType: conversion
validationStatus: COMPLETE
validationDate: 2026-02-12
validationReport: './validation-report-2026-02-12.md'
coverageStatus: complete
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-next-step', 'step-10-confirmation', 'step-11-completion']
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/ocf/workflows/design-orchestration/design-orchestration.spec.md
**Original Format:** BMAD Workflow Specification (placeholder spec)
**Detected Structure:** 5-step create-only workflow spec with agent assignments, document output

---

## Original Workflow Analysis

### Goal (from source)

Design multi-agent communication patterns for an OpenClaw agent system.

### Original Steps (Complete List)

**Step 1:** Agent Map — Map all agents and their relationships
**Step 2:** Communication Design — Define spawn/send patterns and session routing
**Step 3:** Channel Bindings — Configure channel-to-agent routing
**Step 4:** Failure Handling — Design handoff failure patterns and loop prevention
**Step 5:** Subagent Policies — Define tool restrictions for spawned subagents

### Output / Deliverable

Orchestration design document with routing tables, handoff patterns, and failure handling specs.

### Input Requirements

**Required:**
- Agent roster with roles and responsibilities
- Channel requirements

**Optional:**
- Existing orchestration patterns to extend

### Key Instructions to LLM

The spec assigns Vulcan (Forge Master) as primary agent — strategic, methodical, systems architect persona. Cog (Gear Wright) translates orchestration design into configuration. The workflow is facilitative: gathering agent relationships and design decisions from the user, then producing a structured design document.

---

## Conversion Notes

**What works well in original:**
- Clear 5-step progression from mapping → design → configuration → resilience → policy
- Accurate alignment with OpenClaw platform primitives (bindings, sessions_spawn, sessions_send, tool policies)
- Well-scoped: focuses specifically on orchestration, not full agent creation

**What needs improvement:**
- Spec only — no actual step files, templates, or output format defined
- Needs concrete interaction patterns for each step
- Channel bindings step should reference the actual OpenClaw binding syntax

**Compliance gaps identified:**
- No workflow.md entry point
- No step files
- No output template
- No frontmatter standards
- No menu handling patterns

---

## Classification Decisions

**Workflow Name:** design-orchestration
**Target Path:** {bmb_creations_output_folder}/workflows/design-orchestration

**4 Key Decisions:**
1. **Document Output:** true — produces an orchestration design document
2. **Module Affiliation:** OCF (OpenClaw Forge) module
3. **Session Type:** single-session — focused design exercise, not multi-session
4. **Lifecycle Support:** create-only (steps-c/ only)

**Structure Implications:**
- Needs steps-c/ folder only
- No step-01b-continue.md needed
- Single output template for the orchestration design doc
- Standard A/P/C menus on content steps

---

## Requirements

**Flow Structure:**
- Pattern: linear
- Phases: Initialization → Agent Map → Communication Design → Channel Bindings → Failure Handling → Subagent Policies → Assembly
- Estimated steps: 7 (init + 5 core + final assembly/review)

**User Interaction:**
- Style: highly collaborative — Vulcan guides the user through each design decision
- Decision points: agent relationship mapping, spawn vs send choices, channel routing rules, failure strategies, tool restriction levels
- Checkpoint frequency: after each step via standard menu

**Inputs Required:**
- Required: Agent roster (names, roles, responsibilities), channel requirements (which channels, which agents)
- Optional: Existing orchestration patterns, existing openclaw.json for reference
- Prerequisites: Completed agent brief or existing agent definitions

**Output Specifications:**
- Type: document
- Format: structured — clear sections for routing tables, communication patterns, failure handling
- Sections: Agent Map, Communication Patterns, Channel Bindings, Failure Handling, Subagent Policies, Configuration Fragment
- Frequency: single document

**Success Criteria:**
- Every agent has defined communication relationships
- Spawn/send patterns are explicit and justified
- Channel bindings cover all required channels
- Failure handling addresses handoff failures and loop prevention
- Subagent tool restrictions are documented
- Output includes an openclaw.json configuration fragment

**Instruction Style:**
- Overall: mixed — prescriptive for configuration sections (binding syntax, tool policy format), intent-based for design decisions (agent relationships, failure strategies)
- Notes: Reference OpenClaw docs for binding syntax, sessions_spawn parameters, and tool policy format

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** excluded — design workflow doesn't benefit from creative divergence
- **Advanced Elicitation:** included — useful for exploring alternative orchestration patterns
- **Brainstorming:** excluded

**LLM Features:**
- **Web-Browsing:** excluded
- **File I/O:** included — reading existing workspace files, writing output document
- **Sub-Agents:** excluded
- **Sub-Processes:** excluded

**Memory:**
- Type: single-session
- Tracking: stepsCompleted in output frontmatter

**External Integrations:**
- None required

**Installation Requirements:**
- None

---

## Design: Workflow Step Structure

### Step Sequence

| Step | File | Type | Goal |
|------|------|------|------|
| 01 | step-01-init.md | Init (non-continuable) | Load inputs, detect existing workspace files, set up output document |
| 02 | step-02-agent-map.md | Middle (Standard) | Map all agents, their roles, and relationships |
| 03 | step-03-communication.md | Middle (Standard) | Design spawn/send patterns and session routing |
| 04 | step-04-bindings.md | Middle (Standard) | Configure channel-to-agent routing bindings |
| 05 | step-05-failure.md | Middle (Standard) | Design failure handling, handoff patterns, loop prevention |
| 06 | step-06-policies.md | Middle (Standard) | Define subagent tool restrictions and policies |
| 07 | step-07-assembly.md | Final | Assemble complete design document and config fragment |

### Flow Diagram

```
step-01-init → step-02-agent-map → step-03-communication → step-04-bindings → step-05-failure → step-06-policies → step-07-assembly
```

### Interaction Patterns

- Steps 02-06: Standard A/P/C menu — collaborative content creation
- Step 01: Auto-proceed after initialization
- Step 07: Final assembly with review, no next step

### File Structure

```
design-orchestration/
├── workflow.md
├── steps-c/
│   ├── step-01-init.md
│   ├── step-02-agent-map.md
│   ├── step-03-communication.md
│   ├── step-04-bindings.md
│   ├── step-05-failure.md
│   ├── step-06-policies.md
│   └── step-07-assembly.md
├── data/
│   └── openclaw-orchestration-reference.md
└── templates/
    └── orchestration-design-template.md
```

### Data Flow

- Step 01: Loads agent roster + channel requirements → creates output doc from template
- Step 02: Writes Agent Map section to output doc
- Step 03: Writes Communication Patterns section (references agent map)
- Step 04: Writes Channel Bindings section (references agents + channels)
- Step 05: Writes Failure Handling section (references communication patterns)
- Step 06: Writes Subagent Policies section (references agent map + communication patterns)
- Step 07: Assembles final document, generates openclaw.json fragment, final review

### Role Definition

**AI Role:** Systems architect and orchestration designer — Vulcan (Forge Master) persona
**Expertise:** OpenClaw's binding system, session tools, multi-agent routing, tool policies, subagent spawning
**Communication:** Strategic and methodical. Speaks like an architect reviewing blueprints.
**Collaboration:** Guides user through each design decision, presents options with trade-offs, captures decisions in structured format.

---

## Foundation Build Complete

**Created:**
- Folder structure at: {bmb_creations_output_folder}/workflows/design-orchestration
- workflow.md
- Main template: orchestration-design-template.md
- Reference data: openclaw-orchestration-reference.md

**Configuration:**
- Workflow name: design-orchestration
- Continuable: no
- Document output: yes - structured
- Mode: create-only
