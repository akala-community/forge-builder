---
conversionFrom: 'src/modules/ocf/workflows/export-config/export-config.spec.md'
originalFormat: 'OCF workflow spec (.spec.md)'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-step-02', 'step-09-build-step-03', 'step-10-confirmation']
created: 2026-02-11
status: COMPLETE
approvedDate: 2026-02-11
completionDate: 2026-02-11
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/ocf/workflows/export-config/export-config.spec.md
**Original Format:** OCF workflow spec (.spec.md)
**Detected Structure:** Placeholder spec with 3 planned steps, utility type, create-only mode

---

## Original Workflow Analysis

### Goal (from source)

Extract and format openclaw.json fragments ready for merge into an existing OpenClaw installation.

### Original Steps (Complete List)

**Step 1:** Load Workspace - Load workspace and identify all configuration artifacts
**Step 2:** Extract Fragments - Collect all openclaw.json-relevant configuration
**Step 3:** Format Output - Format fragments for merge with clear section markers

### Output / Deliverable

`openclaw-config-{system-name}.json` — Formatted configuration fragments ready for merge into an existing openclaw.json.

### Input Requirements

**Required:** Path to generated workspace
**Optional:** Existing openclaw.json to preview merge result

### Key Instructions to LLM

Cog (Gear Wright) persona — precise, technical, configuration-focused. Speaks in terms of configuration and structure. Collaborative but technically rigorous.

---

## Conversion Notes

**What works well in original:**
- Clear 3-step linear flow
- Well-defined output format (JSON config fragments)
- Specific agent assignment (Cog)
- Clear purpose — extract config for merge

**What needs improvement:**
- Only a placeholder spec — no actual implementation
- Needs deep understanding of openclaw.json schema structure
- Needs to handle all configuration domains (agents, bindings, tools, memory, failover, heartbeat, logging)
- Should support merge preview when existing config is provided

**Compliance gaps identified:**
- No step files exist
- No workflow.md
- No templates or data files
- Needs full BMAD-compliant step-file architecture

---

## Classification Decisions

**Workflow Name:** export-config
**Target Path:** {bmb_creations_output_folder}/workflows/export-config

**4 Key Decisions:**
1. **Document Output:** true — produces JSON configuration fragments document
2. **Module Affiliation:** OCF module (OpenClaw Forge)
3. **Session Type:** single-session — quick utility workflow
4. **Lifecycle Support:** create-only (steps-c/ only)

**Structure Implications:**
- Only needs steps-c/ folder
- No step-01b-continue.md needed
- Simple linear flow with 3 steps
- Document-producing with structured output template

---

## Requirements

**Flow Structure:**
- Pattern: linear
- Phases: Load → Extract → Format
- Estimated steps: 3

**User Interaction:**
- Style: mostly autonomous with checkpoints
- Decision points: workspace path input, optional merge preview, final review
- Checkpoint frequency: after each step

**Inputs Required:**
- Required: Path to generated OpenClaw workspace
- Optional: Path to existing openclaw.json for merge preview

**Output Specifications:**
- Type: document (JSON configuration fragments)
- Format: structured — clear section markers for each configuration domain
- Sections: agents, bindings, tools, memory, model/failover, heartbeat, logging
- Frequency: single output per run

**Success Criteria:**
- All configuration-relevant artifacts extracted from workspace
- JSON fragments are valid and correctly structured per openclaw.json schema
- Section markers clearly identify each configuration domain
- Merge instructions provided for each section
- Optional merge preview shows combined result

**Instruction Style:**
- Overall: mixed — prescriptive for extraction logic, intent-based for user interaction
- Notes: Cog persona throughout, precise technical language

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** excluded — utility workflow, no creative exploration needed
- **Advanced Elicitation:** excluded — straightforward extraction, no deep exploration
- **Brainstorming:** excluded — not applicable

**LLM Features:**
- **Web-Browsing:** excluded — all data comes from workspace files
- **File I/O:** included — must read workspace files and write output
- **Sub-Agents:** excluded — simple linear flow
- **Sub-Processes:** excluded — not needed for 3-step utility

**Memory:**
- Type: single-session
- Tracking: stepsCompleted in output frontmatter

**External Integrations:**
- None

**Installation Requirements:**
- None

---

## Workflow Design

### Step Outline

**Step 01: Load Workspace**
- Type: Init Step (Non-Continuable)
- Goal: Load workspace, inventory all agents, identify all configuration artifacts
- Actions:
  1. Welcome and get workspace path
  2. Load all workspace files (openclaw.json, AGENTS.md, SOUL.md, skills/, agent configs)
  3. Inventory agents with their current configurations
  4. Optionally load existing openclaw.json for merge preview
  5. Create output document from template
  6. Present inventory summary
- Menu: C-only (Continue to Extract)
- Outputs to: Config export document — Workspace Inventory section

**Step 02: Extract Fragments**
- Type: Middle Step (Simple)
- Goal: Extract all openclaw.json-relevant configuration from workspace artifacts
- Actions:
  1. For each agent, extract: identity, model config, memory config, tool policies, heartbeat, logging
  2. Extract bindings from channel configurations
  3. Extract system-wide config (failover, logging, global tools)
  4. Generate JSON fragments per section
  5. Present extracted fragments for review
- Menu: C-only (Continue to Format)
- Outputs to: Config export document — per-domain configuration sections

**Step 03: Format & Complete**
- Type: Final Step
- Goal: Format all fragments for merge, generate merge instructions, optionally preview merge
- Actions:
  1. Assemble all fragments into final structured output
  2. Generate merge instructions for each section
  3. If existing openclaw.json provided, generate merge preview
  4. Present final output summary
  5. Complete workflow
- Menu: None (final step)
- Outputs to: Config export document — final assembly + merge instructions

### File Structure

```
export-config/
├── workflow.md
├── steps-c/
│   ├── step-01-load-workspace.md
│   ├── step-02-extract-fragments.md
│   └── step-03-format-complete.md
├── templates/
│   └── config-export-template.md
└── data/
    └── config-domains.md
```

### Interaction Pattern
- Linear flow, mostly autonomous
- User provides workspace path at start
- Checkpoints after load and extract for review
- Final output presented at completion

### Data Flow
- Step 01 → loads workspace files, creates inventory
- Step 02 → reads inventory, extracts JSON fragments per domain
- Step 03 → assembles fragments, adds merge instructions

### Role and Persona
- Cog (Gear Wright) — precision configuration engineer
- Technical, precise language
- Deep expertise in openclaw.json structure

---

## Foundation Build Complete

**Created:**
- Folder structure at: {bmb_creations_output_folder}/workflows/export-config
- workflow.md
- Main template: config-export-template.md
- Data file: config-domains.md

**Configuration:**
- Workflow name: export-config
- Continuable: no
- Document output: yes - structured
- Mode: create-only
