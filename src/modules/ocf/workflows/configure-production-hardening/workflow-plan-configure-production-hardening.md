---
conversionFrom: 'src/modules/ocf/workflows/configure-production-hardening/configure-production-hardening.spec.md'
originalFormat: 'OCF Workflow Specification (Placeholder)'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-next-step', 'step-10-confirmation', 'step-11-completion']
created: 2026-02-11
completionDate: 2026-02-11
status: COMPLETE
confirmationType: conversion
coverageStatus: complete
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/ocf/workflows/configure-production-hardening/configure-production-hardening.spec.md
**Original Format:** OCF Workflow Specification (Placeholder — spec only, no implementation)
**Detected Structure:** Single spec.md file defining workflow goal, 7 planned steps, inputs/outputs, and agent integration. No existing step files, templates, or data files exist yet.

---

## Original Workflow Analysis

### Goal (from source)

Layer production features onto a generated or existing OpenClaw workspace. Takes a workspace and adds memory configuration, tool policies, failover chains, heartbeat patterns, logging setup, self-correction directives, and boundary rules. Can be run standalone on workspaces not created by OCF.

### Original Steps (Complete List)

**Step 1:** Load Workspace - Load workspace and assess current hardening level
**Step 2:** Memory Config - Configure memory backends with auto-recall/capture per agent
**Step 3:** Tool Policies - Define per-agent allow/deny lists based on role
**Step 4:** Failover & Resilience - Configure model fallback chains and context overflow handling
**Step 5:** Observability - Set up heartbeat patterns, logging config, and monitoring
**Step 6:** Self-Correction - Add error journaling, pre-response checks, and feedback capture
**Step 7:** Boundary Rules - Define privacy rules, escalation triggers, and data handling policies

### Output / Deliverable

- Updated workspace artifacts with production hardening applied
- Hardening report documenting all configurations added

### Input Requirements

**Required:**
- Path to OpenClaw workspace (OCF-generated or existing)

**Optional:**
- Specific hardening features to focus on
- Environment target (development vs production)

### Key Instructions to LLM

The spec defines Cog (Gear Wright) as the primary agent. Cog is a precision engineer who speaks in terms of configuration and structure. The workflow should adopt Cog's technical, precise communication style. Collaborative but technically authoritative. The workflow produces documents (hardening report + updated workspace artifacts).

---

## Conversion Notes

**What works well in original:**
- Clear 7-step decomposition of hardening concerns
- Each step focuses on a distinct hardening domain
- Good separation of concerns (memory, tools, failover, observability, self-correction, boundaries)
- Standalone capability (works on non-OCF workspaces)

**What needs improvement:**
- No implementation exists yet — only a spec placeholder
- Steps need detailed instruction content for each hardening domain
- Needs assessment/audit capability (step 1) to determine what's already configured
- Missing final assembly/review step
- No data files for reference defaults or best practices

**Compliance gaps identified:**
- No step files exist — entire workflow needs to be created from spec
- No frontmatter, no menu patterns, no execution protocols
- No output template for the hardening report
- No data/reference files for hardening defaults
- Missing BMAD step-file architecture entirely

---

## Classification Decisions

**Workflow Name:** configure-production-hardening
**Target Path:** {bmb_creations_output_folder}/workflows/configure-production-hardening

**4 Key Decisions:**
1. **Document Output:** true (produces hardening report + updated workspace config artifacts)
2. **Module Affiliation:** ocf (OpenClaw Forge module)
3. **Session Type:** single-session (each hardening pass is focused and completable in one session)
4. **Lifecycle Support:** create-only (steps-c/ only — hardening is applied once, re-run for updates)

**Structure Implications:**
- Needs steps-c/ folder only
- No step-01b-continue.md needed
- Document output requires output template for hardening report
- Data files needed for hardening defaults/best practices
- 8 steps total (7 from spec + 1 final review/report step)

---

## Requirements

**Flow Structure:**
- Pattern: linear (step through each hardening domain sequentially)
- Phases: Load/Assess, Memory, Tools, Failover, Observability, Self-Correction, Boundaries, Review/Report
- Estimated steps: 8

**User Interaction:**
- Style: mixed (collaborative for assessment/decisions, mostly autonomous for configuration generation)
- Decision points: Step 1 (select scope), each hardening step (approve config before applying)
- Checkpoint frequency: menu at end of each step

**Inputs Required:**
- Required: Path to OpenClaw workspace
- Optional: Specific hardening features to focus on, environment target
- Prerequisites: Existing workspace with at minimum AGENTS.md files

**Output Specifications:**
- Type: document (hardening report)
- Format: structured (sections per hardening domain)
- Sections: Assessment Summary, Memory Config, Tool Policies, Failover Config, Observability Config, Self-Correction Config, Boundary Rules, Overall Status
- Frequency: single (one report per hardening run)

**Success Criteria:**
- All selected hardening domains configured
- Configuration artifacts generated for each domain
- Hardening report documents what was added/changed
- No security gaps in generated configurations

**Instruction Style:**
- Overall: mixed (prescriptive for config generation, intent-based for assessment and user interaction)
- Notes: Cog (Gear Wright) persona — precise, technical, configuration-focused

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** excluded - not applicable for technical configuration workflow
- **Advanced Elicitation:** excluded - configurations are technical, not creative
- **Brainstorming:** excluded - hardening follows established patterns

**LLM Features:**
- **Web-Browsing:** excluded - uses local workspace files only
- **File I/O:** included - reads workspace files, writes configuration artifacts
- **Sub-Agents:** excluded - single-agent workflow (Cog)
- **Sub-Processes:** excluded - linear flow, no parallel needs

**Memory:**
- Type: single-session
- Tracking: stepsCompleted in output report frontmatter

**External Integrations:**
- None required

**Installation Requirements:**
- None beyond standard BMAD installation

---

## Workflow Structure Design

### Step Outline

| Step | File | Type | Goal |
|------|------|------|------|
| 01 | step-01-load-workspace.md | Init (Non-Continuable, Input Discovery) | Load workspace, inventory agents, assess current hardening level |
| 02 | step-02-memory-config.md | Middle (Standard) | Configure memory backends per agent with auto-recall/capture |
| 03 | step-03-tool-policies.md | Middle (Standard) | Define per-agent tool allow/deny lists |
| 04 | step-04-failover.md | Middle (Standard) | Configure model fallback chains and context overflow |
| 05 | step-05-observability.md | Middle (Standard) | Set up heartbeat, logging, and monitoring |
| 06 | step-06-self-correction.md | Middle (Standard) | Add error journaling, pre-response checks, feedback capture |
| 07 | step-07-boundary-rules.md | Middle (Standard) | Define privacy, escalation, and data handling policies |
| 08 | step-08-review-report.md | Final | Assemble hardening report, present summary, complete |

### Data Flow
- Step 01 reads workspace, produces agent inventory + assessment in report
- Steps 02-07 each read assessment, generate config for their domain, append to report
- Step 08 assembles final report with all configurations

### File Structure
```
configure-production-hardening/
├── workflow.md
├── steps-c/
│   ├── step-01-load-workspace.md
│   ├── step-02-memory-config.md
│   ├── step-03-tool-policies.md
│   ├── step-04-failover.md
│   ├── step-05-observability.md
│   ├── step-06-self-correction.md
│   ├── step-07-boundary-rules.md
│   └── step-08-review-report.md
├── data/
│   └── hardening-defaults.md
└── templates/
    └── hardening-report-template.md
```

---

## Foundation Build Complete

**Created:**
- Folder structure at: {bmb_creations_output_folder}/workflows/configure-production-hardening
- workflow.md
- Main template: hardening-report-template.md
- Data: hardening-defaults.md

**Configuration:**
- Workflow name: configure-production-hardening
- Continuable: no
- Document output: yes (structured)
- Mode: create-only
