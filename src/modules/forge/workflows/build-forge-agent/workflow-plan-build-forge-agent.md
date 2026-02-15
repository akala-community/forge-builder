---
conversionFrom: 'src/modules/forge/workflows/build-forge-agent/build-forge-agent.spec.md'
originalFormat: 'spec-placeholder'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-next-step', 'step-10-confirmation', 'step-11-completion']
created: 2026-02-13
status: COMPLETE
completionDate: 2026-02-13
confirmationType: conversion
coverageStatus: complete
approvedDate: 2026-02-13
workflowName: build-forge-agent
targetWorkflowPath: '_bmad/forge/workflows/build-forge-agent/'
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/forge/workflows/build-forge-agent/build-forge-agent.spec.md
**Original Format:** Specification placeholder (single .spec.md file, no executable workflow)
**Detected Structure:** 6-step planned workflow for generating OpenClaw workspace files from agent spec and module context

---

## Original Workflow Analysis

### Goal (from source)

Generate The Forge's complete OpenClaw workspace files — SOUL.md, AGENTS.md, IDENTITY.md, and any other required workspace artifacts. Uses the module brief and agent spec as source material.

### Original Steps (Complete List)

**Step 1:** Load agent spec — Load forge.spec.md and module brief as source material
**Step 2:** Generate SOUL.md — Create personality, lore, and behavioral guidelines
**Step 3:** Generate IDENTITY.md — Create identity card with name, role, capabilities
**Step 4:** Generate AGENTS.md — Create operational instructions and tool usage
**Step 5:** Generate workspace config — Create any additional workspace files needed
**Step 6:** Validate outputs — Cross-check all generated files for consistency

### Output / Deliverable

- `SOUL.md` — Personality, lore, behavioral guidelines (forge-themed)
- `IDENTITY.md` — Identity card (name, creature, vibe, emoji, avatar)
- `AGENTS.md` — Operational instructions (session startup, memory, safety, tools, heartbeats)
- Additional workspace files as needed

### Input Requirements

- `forge.spec.md` — Agent specification with persona, communication style, principles, menu commands
- Module context — module.yaml, README.md, docs/agents.md for broader context
- OpenClaw workspace templates — docs/reference/templates/ for SOUL.md, IDENTITY.md, AGENTS.md format reference

### Key Instructions to LLM

- Code generation workflow — produces concrete file artifacts
- Uses forge metaphors naturally (forging, tempering, quality inspection, blueprints)
- Agent persona is rich: three-master-craftsmen lore, precise yet approachable voice
- Templates provide structure; agent spec provides content to pour into that structure
- Morgan (Forge Builder) is the primary agent executing this workflow

---

## Conversion Notes

**What works well in original:**
- Clear step progression from loading inputs to generating each file to validation
- Well-defined output artifacts with distinct purposes
- Rich source material in the agent spec for content generation
- Good separation of concerns (each output file has its own generation step)

**What needs improvement:**
- No executable workflow exists — only a spec placeholder
- No detailed instructions for what each generated file should contain
- No collaborative interaction points — purely autonomous generation
- Missing guidance on how to handle the forge lore/personality translation
- No output path configuration

**Compliance gaps identified:**
- No step files exist (need full steps-c/ folder)
- No workflow.md entry point
- No frontmatter or state tracking
- No menu/continuation points defined
- No validation criteria specified for step 6

---

## Classification Decisions

**Workflow Name:** build-forge-agent
**Target Path:** _bmad/forge/workflows/build-forge-agent/

**4 Key Decisions:**
1. **Document Output:** true (produces SOUL.md, IDENTITY.md, AGENTS.md, and additional workspace files)
2. **Module Affiliation:** forge
3. **Session Type:** single-session
4. **Lifecycle Support:** create-only

**Structure Implications:**
- Needs `steps-c/` folder only (no steps-e/ or steps-v/)
- No continuation logic needed (no step-01b-continue.md)
- Standard init step (no continuable frontmatter tracking)
- Multiple output files rather than single document — each step generates a distinct file
- Output files written to configured forge_artifacts path

---

## Requirements

**Flow Structure:**
- Pattern: linear (plan-then-build)
- Phases: Load inputs → Generate SOUL.md → Generate IDENTITY.md → Generate AGENTS.md → Generate extras → Validate
- Estimated steps: 6

**User Interaction:**
- Style: mostly autonomous with checkpoints
- Decision points: After each file generation, user reviews and approves before proceeding
- Checkpoint frequency: After each generated file

**Inputs Required:**
- Required: forge.spec.md (agent specification)
- Required: OpenClaw workspace templates (docs/reference/templates/SOUL.md, IDENTITY.md, AGENTS.md)
- Optional: Module context (module.yaml, README.md, docs/)
- Optional: Existing workspace files to merge with
- Optional: Custom personality overrides
- Prerequisites: forge module must exist with agent spec file

**Output Specifications:**
- Type: multiple distinct document files
- Format: structured (each file follows its OpenClaw template skeleton)
- Files:
  - SOUL.md — Core Truths, Boundaries, Vibe, Continuity (forge-themed)
  - IDENTITY.md — Name, Creature, Vibe, Emoji, Avatar
  - AGENTS.md — First Run, Every Session, Memory, Safety, Tools, Heartbeats (forge-customized)
  - Additional workspace config as needed
- Output path: {forge_artifacts}/workspace/

**Success Criteria:**
- All 3 core workspace files generated (SOUL.md, IDENTITY.md, AGENTS.md)
- Each file follows its OpenClaw template structure correctly
- Forge personality and lore consistently reflected across all files
- Forge metaphors used naturally (forging, tempering, quality inspection, blueprints)
- No contradictions between files
- Files are ready to drop into an OpenClaw workspace

**Instruction Style:**
- Overall: prescriptive
- Notes: Code generation workflow — clear inputs (spec + template) produce clear outputs (specific file). Creative latitude only in how forge personality is expressed within template sections.

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** excluded — Prescriptive generation workflow, not creative brainstorming
- **Advanced Elicitation:** excluded — Inputs well-defined from spec and templates
- **Brainstorming:** excluded — Content comes from source material, not ideation

**LLM Features:**
- **File I/O:** included — Core to workflow; every step reads source files and writes output files
- **Web-Browsing:** excluded — All source material is local
- **Sub-Agents:** excluded — Sequential file generation from same source
- **Sub-Processes:** excluded — Files generated sequentially for consistency

**Memory:**
- Type: single-session
- Tracking: None needed (no continuation)

**External Integrations:**
- None required — All inputs and outputs are local markdown files

**Installation Requirements:**
- None — All tools are built-in file operations

**Workflow Structure Preview:**

Phase 1: Initialization & Source Loading
- Load forge.spec.md, OpenClaw workspace templates, optional module context
- Validate all required inputs present
- Present summary to user

Phase 2: Generate SOUL.md
- Map forge persona to SOUL.md template structure
- Write file, present for review

Phase 3: Generate IDENTITY.md
- Extract identity fields from spec
- Write file, present for review

Phase 4: Generate AGENTS.md
- Map forge operational patterns to AGENTS.md template
- Write file, present for review

Phase 5: Generate Additional Workspace Files
- Determine and generate extras (TOOLS.md, HEARTBEAT.md, etc.)
- Present for review

Phase 6: Cross-File Validation
- Check personality consistency, contradictions, missing references
- Present validation report and final summary
