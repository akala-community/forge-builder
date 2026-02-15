---
conversionFrom: 'src/modules/ocf/workflows/edit-agent-system/edit-agent-system.spec.md'
originalFormat: 'BMAD Module Specification (placeholder)'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-next-step', 'step-10-confirmation', 'step-11-completion']
created: 2026-02-11
status: COMPLETE
completionDate: 2026-02-11
confirmationType: conversion
coverageStatus: complete
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/ocf/workflows/edit-agent-system/edit-agent-system.spec.md
**Original Format:** BMAD Module Specification (placeholder -- no implementation)
**Detected Structure:** Specification document with goal, 5-step outline, inputs/outputs, and agent assignments. No step files, templates, or implementation exist.

---

## Original Workflow Analysis

### Goal (from source)

Modify an existing generated workspace while maintaining coherence across all artifacts. Change one agent's persona, skills, or configuration and propagate implications to memory scaffolds, tool policies, directives, and other interconnected artifacts. Ensures the system stays internally consistent after edits.

### Original Steps (Complete List)

**Step 1:** Load Workspace - Load existing workspace and inventory all artifacts
**Step 2:** Identify Changes - Determine what the user wants to modify
**Step 3:** Impact Analysis - Analyze which artifacts are affected by the change
**Step 4:** Apply Changes - Modify artifacts and propagate implications
**Step 5:** Coherence Check - Verify internal consistency after edits

### Output / Deliverable

- Updated workspace artifacts (in-place modifications to AGENTS.md, SOUL.md, USER.md, MEMORY.md, skills/, openclaw.json, tool policies, etc.)
- Change report documenting what was modified and why

### Input Requirements

**Required:**
- Path to existing generated workspace
- Description of desired changes

**Optional:**
- Specific artifacts to modify

### Key Instructions to LLM

The spec does not define instruction patterns (it's a placeholder). Based on the OCF module patterns and sibling workflows:
- Dual-agent model: Anima handles persona/identity changes, Cog handles config/skill changes
- Vulcan consulted for architectural implications
- Collaborative facilitation style consistent with OCF workflows
- File I/O heavy: reads and modifies existing workspace artifacts in-place

---

## Conversion Notes

**What works well in original:**
- Clear 5-step flow from load to verify
- Dual-agent assignment aligns with OCF architecture (Anima for soul, Cog for gear)
- Impact analysis step prevents cascading inconsistencies
- Coherence check mirrors validate-workspace capability

**What needs improvement:**
- Steps are high-level outlines -- need detailed instructions for each
- No guidance on HOW to inventory artifacts or perform impact analysis
- No specification of the change report format
- No error handling for invalid workspace paths or corrupt artifacts

**Compliance gaps identified:**
- No step files exist (placeholder spec only)
- No workflow.md entry point
- No frontmatter, menu handling, or state tracking
- No templates or data files
- No continuation support design
- No subprocess optimization consideration

---

## Classification Decisions

**Workflow Name:** edit-agent-system
**Target Path:** {bmb_creations_output_folder}/workflows/edit-agent-system (build), {project-root}/_bmad/ocf/workflows/edit-agent-system (installed)

**4 Key Decisions:**
1. **Document Output:** true -- produces a Change Report documenting modifications
2. **Module Affiliation:** OCF (OpenClaw Forge) -- Feature workflow in the OCF module
3. **Session Type:** Continuable -- complex multi-artifact edits may span sessions
4. **Lifecycle Support:** Create-only (steps-c/) -- this IS the edit workflow for agent systems; validate-workspace serves as validation counterpart

**Structure Implications:**
- Needs steps-c/ folder only
- Needs step-01-init.md with continuation detection
- Needs step-01b-continue.md for resuming
- Needs stepsCompleted tracking in change report frontmatter
- Output template for the change report document
- File I/O required for reading/modifying workspace artifacts
- Input discovery needed to locate existing workspace artifacts

---

## Requirements

**Flow Structure:**
- Pattern: Linear with potential looping (Apply Changes may iterate if user wants multiple edits)
- Phases:
  1. Initialization & Workspace Loading
  2. Change Identification (collaborative)
  3. Impact Analysis (mostly autonomous with review)
  4. Change Application (autonomous with confirmation gates)
  5. Coherence Verification (autonomous with report)
- Estimated steps: 6 (init + 5 core steps)

**User Interaction:**
- Style: Mixed -- collaborative during change identification, mostly autonomous during impact analysis and application, with confirmation gates
- Decision points:
  - What to change (user drives)
  - Approve impact analysis before applying
  - Confirm each artifact modification
  - Accept or iterate after coherence check
- Checkpoint frequency: After each major phase

**Inputs Required:**
- Required:
  - Path to existing OCF-generated workspace (directory containing AGENTS.md, SOUL.md, etc.)
  - Description of desired changes (natural language)
- Optional:
  - Specific agent name to modify (if multi-agent workspace)
  - Specific artifact type to focus on (persona, skills, config, etc.)
- Prerequisites:
  - Workspace must have been generated by create-agent-system or create-single-agent workflow (or follow OCF workspace structure)

**Output Specifications:**
- Type: Document (Change Report) + in-place file modifications
- Format: Structured -- the change report needs clear sections for traceability
- Sections:
  - Workspace Summary (what was loaded)
  - Changes Requested
  - Impact Analysis Results
  - Modifications Applied (per-artifact diff summary)
  - Coherence Check Results
  - Recommendations for further changes
- Frequency: Single report per edit session

**Success Criteria:**
- All requested changes applied correctly to workspace artifacts
- No coherence violations introduced (or all flagged and addressed)
- Change report accurately documents all modifications
- Workspace passes validate-workspace checks after edits
- User confirms the edits match their intent

**Instruction Style:**
- Overall: Mixed
- Step 01 (Load): Intent-based -- flexible loading and inventory
- Step 02 (Identify): Collaborative/prescriptive -- structured change gathering
- Step 03 (Impact): Intent-based -- autonomous analysis with structured output
- Step 04 (Apply): Prescriptive -- precise file modifications with confirmation gates
- Step 05 (Coherence): Intent-based -- autonomous verification with structured report

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** excluded -- edit workflow requires precision, not creative brainstorming
- **Advanced Elicitation:** included -- Integration point: Step 02 (Identify Changes) for deep exploration of what user wants to change
- **Brainstorming:** excluded -- edits are targeted, not generative

**LLM Features:**
- **Web-Browsing:** excluded -- workspace editing is entirely local
- **File I/O:** included -- Core requirement. Must read all workspace artifacts, modify them in-place, and write the change report
- **Sub-Agents:** excluded -- single-threaded edit flow
- **Sub-Processes:** included -- Pattern 2 (Per-file deep analysis) for impact analysis across multiple artifacts. Pattern 4 (Parallel) for coherence checks across artifacts

**Memory:**
- Type: Continuable
- Tracking: stepsCompleted in change report frontmatter, lastStep, workspace path persistence

**External Integrations:**
- None required -- all operations are local file I/O

**Installation Requirements:**
- No additional tools need installation
- User preference: N/A

---

## Plan Review

**Plan approved for design (YOLO mode).**

All sections reviewed:
- Vision/scope: Clear -- edit existing OCF workspaces with coherence
- Structural decisions: Confirmed -- document-producing, OCF module, continuable, create-only
- Requirements: Complete -- linear+loop flow, mixed interaction, structured change report
- Tools: Appropriate -- File I/O essential, subprocess for analysis, Advanced Elicitation for change gathering

---

## Workflow Structure Design

### Step Outline

| Step | File | Type | Goal |
|------|------|------|------|
| 01 | step-01-init.md | Init (Continuable) | Load workspace, inventory artifacts, validate structure |
| 01b | step-01b-continue.md | Continuation | Resume from previous session |
| 02 | step-02-identify-changes.md | Middle (Standard) | Collaboratively determine what the user wants to modify |
| 03 | step-03-impact-analysis.md | Middle (Standard) | Analyze cross-artifact implications of requested changes |
| 04 | step-04-apply-changes.md | Middle (Standard) | Apply modifications to artifacts with confirmation gates |
| 05 | step-05-coherence-check.md | Middle (Standard) | Verify workspace consistency post-edit, option to iterate |
| 06 | step-06-completion.md | Final | Present change report summary, offer validate-workspace chaining |

### Flow Diagram

```
step-01-init (load workspace)
  ├── [existing output found] → step-01b-continue → route to next incomplete step
  └── [fresh start] → step-02-identify-changes
                         ↓
                    step-03-impact-analysis
                         ↓
                    step-04-apply-changes
                         ↓
                    step-05-coherence-check
                         ├── [issues found] → loop back to step-02 or step-04
                         └── [clean] → step-06-completion
```

### Interaction Patterns

- **Step 01:** Auto-proceed after loading (C-only menu)
- **Step 02:** A/P/C menu (Advanced Elicitation available for deep change exploration)
- **Step 03:** C-only menu (autonomous analysis with review)
- **Step 04:** C-only menu (modifications shown for confirmation before proceeding)
- **Step 05:** Custom menu: [C] Complete / [E] Edit More (loop to step-02) / [F] Fix Issues (loop to step-04)
- **Step 06:** Final step -- no next step

### Data Flow

- **Step 01 → 02:** Workspace inventory (artifact list, agent roster, current state)
- **Step 02 → 03:** Change description (structured: what to change, on which agent, which artifact types)
- **Step 03 → 04:** Impact map (which files need modification, what changes in each, cross-references)
- **Step 04 → 05:** Applied changes summary (before/after for each modified artifact)
- **Step 05 → 06:** Coherence results (pass/fail per check, recommendations)

### File Structure

```
edit-agent-system/
├── workflow.md
├── steps-c/
│   ├── step-01-init.md
│   ├── step-01b-continue.md
│   ├── step-02-identify-changes.md
│   ├── step-03-impact-analysis.md
│   ├── step-04-apply-changes.md
│   ├── step-05-coherence-check.md
│   └── step-06-completion.md
├── data/
│   ├── artifact-types.csv
│   ├── coherence-rules.csv
│   └── impact-matrix.csv
└── templates/
    └── change-report-template.md
```

### Data Files

**artifact-types.csv:** Defines the OCF workspace artifact types, their file patterns, and interdependencies
- Columns: artifact_type, file_pattern, description, depends_on, affected_by

**coherence-rules.csv:** Defines cross-artifact consistency rules
- Columns: rule_id, source_artifact, target_artifact, check_type, description, severity

**impact-matrix.csv:** Maps change types to affected artifacts
- Columns: change_type, primary_artifact, secondary_artifacts, propagation_rule

### Role and Persona

The AI embodies a dual role matching the OCF agent architecture:
- **For persona/identity changes:** Acts as Anima (Soul Smith) -- creative, empathetic, focused on coherent personality
- **For config/skill changes:** Acts as Cog (Gear Wright) -- precise, technical, focused on configuration rigor
- **For architectural implications:** Channels Vulcan (Forge Master) -- strategic, methodical, systems-level thinking

Communication style: Precise but collaborative. Shows the user exactly what will change and why before modifying anything.

### Subprocess Optimization

**Step 03 (Impact Analysis):** Pattern 2 -- Per-artifact subprocess for deep analysis
- For EACH artifact in the workspace, launch a subprocess that analyzes how the requested change affects it
- Subprocess returns: affected (yes/no), specific impacts (list), required modifications (list)
- Fallback: Sequential analysis in main thread

**Step 05 (Coherence Check):** Pattern 4 -- Parallel execution of coherence checks
- Launch parallel subprocesses for each coherence rule category
- Each subprocess checks one category and returns findings
- Fallback: Sequential checks in main thread

---

## Foundation Build Complete

**Created:**
- Folder structure at: {bmb_creations_output_folder}/workflows/edit-agent-system
- workflow.md
- templates/change-report-template.md

**Configuration:**
- Workflow name: edit-agent-system
- Continuable: yes
- Document output: yes (Structured change report)
- Mode: create-only (steps-c/)

---

## Step 01 Build Complete

**Created:**
- steps-c/step-01-init.md (Init - Continuable with input discovery)
- steps-c/step-01b-continue.md (Continuation handler)

**Step Configuration:**
- Type: Init (Continuable)
- Input Discovery: yes (workspace path from user)
- Next Step: step-02-identify-changes

---

## Step 02 Build Complete

**Created:**
- steps-c/step-02-identify-changes.md

**Step Configuration:**
- Type: Middle (Standard) with A/C menu
- Outputs to: Change specifications in change report
- Next Step: step-03-impact-analysis

---

## Step 03 Build Complete

**Created:**
- steps-c/step-03-impact-analysis.md

**Step Configuration:**
- Type: Middle (Standard) with C-only menu
- Subprocess optimization: Pattern 2 (per-artifact analysis)
- Outputs to: Impact analysis results in change report
- Next Step: step-04-apply-changes

---

## Step 04 Build Complete

**Created:**
- steps-c/step-04-apply-changes.md

**Step Configuration:**
- Type: Middle (Standard) with per-file confirmation gates
- Outputs to: Modification records in change report + workspace file modifications
- Next Step: step-05-coherence-check

---

## Step 05 Build Complete

**Created:**
- steps-c/step-05-coherence-check.md

**Step Configuration:**
- Type: Middle (Standard) with custom menu (C/E/F)
- Subprocess optimization: Pattern 4 (parallel coherence checks)
- Outputs to: Coherence results in change report
- Next Step: step-06-completion (or loop to step-02/step-04)

---

## Step 06 Build Complete

**Created:**
- steps-c/step-06-completion.md

**Step Configuration:**
- Type: Final
- Outputs to: Completion summary in change report
- Next Step: none (final step)

---

## Data Files Created

**Created:**
- data/artifact-types.csv (13 artifact types with dependencies)
- data/coherence-rules.csv (14 coherence rules with severities)
- data/impact-matrix.csv (14 change types with propagation rules)

---

## Conversion Coverage Report

**Source:** src/modules/ocf/workflows/edit-agent-system/edit-agent-system.spec.md
**Target:** {bmb_creations_output_folder}/workflows/edit-agent-system

**Overall Coverage:** 100%

| Category | Total | Covered | Partial | Missing |
|----------|-------|---------|---------|---------|
| Goal | 1 | 1 | 0 | 0 |
| Steps | 5 | 5 | 0 | 0 |
| Instructions | N/A | N/A | N/A | N/A |
| Output | 1 | 1 | 0 | 0 |

**Improvements Made:**
- Added continuation support (step-01b-continue.md)
- Added completion step (step-06-completion.md) not in original spec
- Created 3 data files for structured analysis (artifact-types, coherence-rules, impact-matrix)
- Added subprocess optimization for impact analysis and coherence checks
- Added confirmation gates in apply-changes step
- Added loop-back capability from coherence check to identify-changes or apply-changes
- Added Advanced Elicitation integration in identify-changes step
- Dual-agent persona channeling (Anima/Cog/Vulcan) based on change type
