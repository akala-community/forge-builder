---
conversionFrom: 'src/modules/forge/workflows/add-forge-skill/add-forge-skill.spec.md'
originalFormat: 'BMAD spec placeholder'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-next-step', 'step-10-confirmation', 'step-11-completion']
created: 2026-02-14
status: COMPLETE
approvedDate: 2026-02-14
completionDate: 2026-02-14
confirmationType: conversion
coverageStatus: complete
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/forge/workflows/add-forge-skill/add-forge-skill.spec.md
**Original Format:** BMAD workflow specification placeholder
**Detected Structure:** Single spec file with goal, planned steps table (7 steps), inputs/outputs, agent integration, and post-workflow pipeline notes

---

## Original Workflow Analysis

### Goal (from source)

Define a new skill for The Forge and register it in the Forge Builder's build pipeline. Accepts a new skill concept from the user, generates its complete SKILL.md specification and bundled resource requirements, then registers it as a build target in Morgan's (Forge Builder) pipeline.

### Original Steps (Complete List)

**Step 1:** Define skill concept - Gather skill name, purpose, triggers, and scope from user
**Step 2:** Load module context - Load forge.spec.md, forge-builder.spec.md, existing skills list, and module brief
**Step 3:** Generate skill spec - Create the skill's SKILL.md definition with triggers, flow, instructions, and bundled resource requirements
**Step 4:** Register in Forge Builder - Update forge-builder.spec.md to add the new skill as a build-forge-skill target
**Step 5:** Update module artifacts - Update module.yaml, module-help.csv, and docs/workflows.md to reflect the new skill
**Step 6:** Validate consistency - Cross-check the new skill against existing skills for naming collisions, trigger conflicts, and pattern overlap
**Step 7:** Prompt rebuild - Inform user that build-forge-agent should be run next to regenerate The Forge's workspace files

### Output / Deliverable

- `skills/{skill-name}/SKILL.md` - New skill specification
- Updated `forge-builder.spec.md` - New build target registered in Morgan's command table
- Updated `module-help.csv` - New skill entry
- Updated `docs/workflows.md` - Documentation for the new skill

### Input Requirements

**Required:**
- Skill name and description (from user)
- forge.spec.md (The Forge agent specification)
- forge-builder.spec.md (Morgan's agent specification)
- Existing skill specs in skills/ directory (for conflict detection)
- module-brief-forge.md (module brief)

**Optional:**
- Agentic patterns library (if the skill relates to a specific pattern)
- OpenClaw config schema reference (if the skill produces config)
- Example usage scenarios

### Key Instructions to LLM

- Collaborative approach: user defines the concept, agent generates the spec
- Pattern alignment: follow the SKILL.md format established by build-forge-skill
- Registration: update Morgan's command table and module artifacts
- Validation: cross-check against existing skills for conflicts
- Pipeline awareness: inform user about the downstream build pipeline

---

## Conversion Notes

**What works well in original:**
- Clear 7-step pipeline from concept to registration
- Well-defined inputs and outputs
- Pipeline awareness (add -> build-skill -> build-agent)
- Separation of concerns between generation and registration

**What needs improvement:**
- Step 3 (Generate skill spec) is large — covers SKILL.md + bundled resources
- No explicit user review/confirmation gates
- No mechanism for loading existing skill format as reference

**Compliance gaps identified:**
- No BMAD step-file architecture (no steps-c/ folder, no step files)
- No workflow.md entry point
- No frontmatter with state tracking
- No menu options / continuation gates
- No mandatory execution rules
- No success/failure metrics per step
- No output file tracking

---

## Classification Decisions

**Workflow Name:** add-forge-skill
**Target Path:** {project-root}/_bmad/forge/workflows/add-forge-skill/

**4 Key Decisions:**
1. **Document Output:** true (produces SKILL.md + updates to forge-builder.spec.md, module-help.csv, docs/workflows.md)
2. **Module Affiliation:** forge
3. **Session Type:** single-session (7 focused steps, manageable in one session)
4. **Lifecycle Support:** create-only (steps-c/ only, per spec)

**Structure Implications:**
- Needs `steps-c/` folder only (no steps-e/ or steps-v/)
- No continuation step needed (single-session)
- Output file tracks progress through frontmatter stepsCompleted
- Uses forge module config.yaml for variables (forge_artifacts, etc.)
- Installed to `{project-root}/_bmad/forge/workflows/add-forge-skill/`

---

## Requirements

**Flow Structure:**
- Pattern: linear (step 1 through 7, straight through)
- Phases: Discovery (step 1), Context Loading (step 2), Generation (step 3), Registration (steps 4-5), Validation (step 6), Completion (step 7)
- Estimated steps: 7

**User Interaction:**
- Style: mixed (collaborative for concept definition in step 1, mostly autonomous for context loading/generation/registration, collaborative for review gates)
- Decision points: skill concept definition (step 1), skill spec review (step 3), validation findings (step 6)
- Checkpoint frequency: after each major step via Continue menu

**Inputs Required:**
- Required: Skill name and description (user), forge.spec.md, forge-builder.spec.md, existing skills in skills/, module-brief-forge.md
- Optional: Agentic patterns library, OpenClaw config schema reference, example usage scenarios
- Prerequisites: forge module must exist with agent specs and module brief

**Output Specifications:**
- Type: document (primary: SKILL.md) + file modifications (forge-builder.spec.md, module-help.csv, docs/workflows.md)
- Format: structured (SKILL.md follows the established format from build-forge-skill)
- Sections: frontmatter, Triggers, Execution Flow, Instructions, Data Dependencies, Connected Skills, Success Criteria
- Frequency: single (one skill per workflow execution)

**Success Criteria:**
- Valid SKILL.md created following established format
- Skill registered in forge-builder.spec.md command table
- Module artifacts updated (module-help.csv, docs/workflows.md)
- No naming collisions or trigger conflicts with existing skills
- User informed about downstream pipeline (build-forge-skill -> build-forge-agent)

**Instruction Style:**
- Overall: mixed
- Notes: Step 1 (concept definition) is collaborative/intent-based; Steps 2-5 are prescriptive/autonomous; Step 6 (validation) is prescriptive with findings; Step 7 is informational

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** excluded - not needed for this build-focused workflow
- **Advanced Elicitation:** excluded - concept definition is handled collaboratively in step 1
- **Brainstorming:** excluded - skill concepts come from the user

**LLM Features:**
- **Web-Browsing:** excluded - all context is local module files
- **File I/O:** included - reads agent specs, existing skills, writes SKILL.md and updates forge-builder.spec.md
- **Sub-Agents:** excluded - workflow is sequential and focused
- **Sub-Processes:** included - Pattern 3 for loading large context files (module brief, agent specs)

**Memory:**
- Type: single-session
- Tracking: stepsCompleted in output file frontmatter

**External Integrations:**
- None

**Installation Requirements:**
- None

---

## Workflow Structure Design

### Step Sequence (7 steps)

| Step | File | Type | Goal | Menu |
|------|------|------|------|------|
| 01 | step-01-define-concept.md | Middle/Standard | Gather skill name, purpose, triggers, scope from user | C only |
| 02 | step-02-load-context.md | Middle/Simple | Load forge.spec.md, forge-builder.spec.md, existing skills, module brief | Auto-proceed |
| 03 | step-03-generate-spec.md | Middle/Standard | Generate SKILL.md with triggers, flow, instructions, data deps | C only |
| 04 | step-04-register-skill.md | Middle/Simple | Update forge-builder.spec.md command table with new skill | C only |
| 05 | step-05-update-artifacts.md | Middle/Simple | Update module-help.csv and docs/workflows.md | C only |
| 06 | step-06-validate.md | Middle/Standard | Cross-check against existing skills for conflicts | C only |
| 07 | step-07-complete.md | Final | Inform user about pipeline and next steps | Done |

### Data Flow

- Step 01 -> Output file created with skill concept details in frontmatter
- Step 02 -> Context appended to output file (agent specs, existing skills list)
- Step 03 -> SKILL.md generated and written to skills/{skill-name}/SKILL.md
- Step 04 -> forge-builder.spec.md updated with new command table entry
- Step 05 -> module-help.csv and docs/workflows.md updated
- Step 06 -> Validation report appended to output file
- Step 07 -> Summary and next steps presented

### File Structure

```
_bmad/forge/workflows/add-forge-skill/
  workflow.md
  steps-c/
    step-01-define-concept.md
    step-02-load-context.md
    step-03-generate-spec.md
    step-04-register-skill.md
    step-05-update-artifacts.md
    step-06-validate.md
    step-07-complete.md
```

### Role and Persona

Morgan (Forge Builder) - module build engineer, structured and competent, focused on correctness and completeness.

### Subprocess Optimization

- Step 02: Pattern 3 (data loading) for module brief and agent specs
- Step 06: Pattern 4 (parallel) for running multiple validation checks simultaneously

### Workflow Chaining

Pipeline: add-forge-skill -> build-forge-skill -> build-forge-agent
After completion, prompt user to run build-forge-skill then build-forge-agent.

---

## Conversion Coverage Report

**Source:** src/modules/forge/workflows/add-forge-skill/add-forge-skill.spec.md
**Target:** _bmad-output/bmb-creations/workflows/add-forge-skill/

**Overall Coverage: 100%**

| Original Step | Purpose | Covered In | Status |
|---|---|---|---|
| 01: Define skill concept | Gather name, purpose, triggers, scope | step-01-define-concept.md | PASS |
| 02: Load module context | Load agent specs, skills, module brief | step-02-load-context.md | PASS |
| 03: Generate skill spec | Create SKILL.md definition | step-03-generate-spec.md | PASS |
| 04: Register in Forge Builder | Update forge-builder.spec.md command table | step-04-register-skill.md | PASS |
| 05: Update module artifacts | Update module-help.csv, docs/workflows.md | step-05-update-artifacts.md | PASS |
| 06: Validate consistency | Cross-check for conflicts | step-06-validate.md | PASS |
| 07: Prompt rebuild | Inform about build pipeline | step-07-complete.md | PASS |

**Improvements over original:**
- BMAD-compliant micro-file step architecture
- Frontmatter state tracking (stepsCompleted)
- User confirmation gates at every major step
- Subprocess optimization for context loading (Pattern 3) and validation (Pattern 4)
- Success/failure metrics per step
- Structured output file tracking
- 6-check validation framework (structural, naming, triggers, registration, docs, connected skills)

---

## Build Summary

**Files Created:**
- workflow.md (entry point)
- 7 step files in steps-c/

**Workflow is ready for installation at:** {project-root}/_bmad/forge/workflows/add-forge-skill/
