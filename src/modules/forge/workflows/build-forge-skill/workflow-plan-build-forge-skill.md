---
conversionFrom: 'src/modules/forge/workflows/build-forge-skill/build-forge-skill.spec.md'
originalFormat: 'BMAD Workflow Specification (placeholder)'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-steps-02-05', 'step-10-confirmation', 'step-11-completion']
created: 2026-02-13
completionDate: 2026-02-13
status: COMPLETE
approvedDate: 2026-02-13
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/forge/workflows/build-forge-skill/build-forge-skill.spec.md
**Original Format:** BMAD Workflow Specification (placeholder — not yet implemented)
**Detected Structure:** Single spec document with planned steps table, input/output specs, and agent associations. No step files, templates, or data files exist yet.

---

## Original Workflow Analysis

### Goal (from source)

Generate a specific OpenClaw skill's SKILL.md and bundled reference resources. Takes a skill name (one of the 9 OpenClaw skills The Forge provides) and generates its complete SKILL.md definition plus any bundled reference data the skill needs. Each skill is a self-contained capability that The Forge agent activates at runtime.

### Original Steps (Complete List)

**Step 1:** Select skill - Choose which skill to build from the 9 available (design-system, add-agent, recommend-pattern, setup-knowledge, setup-harness, harden-workspace, validate-workspace, export-package, import-package)
**Step 2:** Load skill context - Load relevant brief sections, pattern library, config schema
**Step 3:** Generate SKILL.md - Create the skill definition with triggers, flow, and instructions
**Step 4:** Bundle resources - Generate any reference data the skill needs at runtime
**Step 5:** Validate skill - Check skill for completeness and consistency

### Output / Deliverable

- `skills/{skill-name}/SKILL.md` — Skill definition document
- `skills/{skill-name}/data/` — Bundled reference resources (if needed by the skill)

### Input Requirements

**Required:**
- Skill name (one of: design-system, add-agent, recommend-pattern, setup-knowledge, setup-harness, harden-workspace, validate-workspace, export-package, import-package)
- module-brief-forge.md (module brief for context)
- Agentic patterns library (for pattern-related skills)

**Optional:**
- OpenClaw config schema reference
- Existing skill files to update

### Key Instructions to LLM

The spec is a placeholder — no LLM instruction patterns exist yet. The spec indicates:
- Create-only mode (steps-c/ only, no edit or validate modes)
- Primary agent is Forge Builder (Morgan)
- Workflow type is Build / Code Generation
- Web bundle enabled
- Installed path: `{project-root}/_bmad/forge/workflows/build-forge-skill`

---

## Conversion Notes

**What works well in original:**
- Clear 5-step progression from selection through validation
- Well-defined input/output specifications
- Clean skill enumeration (all 9 skills listed)
- Clear agent assignment (Forge Builder / Morgan)

**What needs improvement:**
- No actual step file content exists — this is a spec, not an implementation
- No templates for SKILL.md output format defined
- No data loading instructions for context gathering (step 2)
- No validation criteria defined (step 5)
- No collaborative facilitation patterns — needs interactive dialogue design

**Compliance gaps identified:**
- No step files exist (need steps-c/ folder with step-01 through step-05)
- No frontmatter in workflow entry point
- No MANDATORY EXECUTION RULES per step
- No menu handling or continuation logic
- No state tracking via stepsCompleted
- No EXECUTION PROTOCOLS defined
- No CONTEXT BOUNDARIES defined
- No success/failure metrics per step

---

## Classification Decisions

**Workflow Name:** build-forge-skill
**Target Path:** {project-root}/_bmad/forge/workflows/build-forge-skill/

**4 Key Decisions:**
1. **Document Output:** true (produces SKILL.md + bundled data/)
2. **Module Affiliation:** forge (module-based)
3. **Session Type:** single-session
4. **Lifecycle Support:** create-only (steps-c/ only)

**Structure Implications:**
- Single `steps-c/` folder with step-01 through step-05
- Standard init (no continuation logic needed)
- No steps-e/ or steps-v/ folders
- Free-form document output template for SKILL.md
- Module variables available from forge module

---

## Requirements

**Flow Structure:**
- Pattern: Linear with repeat option ("Build another skill?")
- Phases: Selection → Context Loading → Generation → Bundling → Validation
- Estimated steps: 5 (step-01 through step-05)

**User Interaction:**
- Style: Mixed — prescriptive selection (step 1), mostly autonomous generation (steps 2-4), autonomous validation (step 5)
- Decision points: Skill selection (step 1), confirm generation before writing (step 3), confirm bundle contents (step 4)
- Checkpoint frequency: Menu after each step

**Inputs Required:**
- Required: Skill name (enumerated list of 9), module-brief-forge.md, agentic patterns library
- Optional: OpenClaw config schema reference, existing skill files to update
- Prerequisites: Module brief must exist

**Output Specifications:**
- Type: Document (SKILL.md) + optional data files
- Format: Structured — SKILL.md has defined sections (triggers, flow, instructions)
- Pattern: Plan-then-build — load context into plan, then generate SKILL.md from accumulated context
- Output path: skills/{skill-name}/SKILL.md and skills/{skill-name}/data/

**Success Criteria:**
- SKILL.md contains complete trigger definitions, execution flow, and instructions
- SKILL.md references match module brief skill descriptions
- Bundled data files generated where skill requires runtime reference data
- Validation passes consistency checks (triggers match flow, flow matches instructions)

**Instruction Style:**
- Overall: Mixed
- Step 1 (Select): Prescriptive — present 9 skills, user picks
- Step 2 (Load): Autonomous — AI loads and organizes context
- Step 3 (Generate): Autonomous with checkpoint — AI generates SKILL.md, user confirms
- Step 4 (Bundle): Autonomous with checkpoint — AI generates data files, user confirms
- Step 5 (Validate): Autonomous — AI runs checks, presents report

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** Excluded — focused generation workflow, no creative exploration needed
- **Advanced Elicitation:** Excluded — requirements are pre-defined in module brief
- **Brainstorming:** Excluded — skills are pre-defined, not being invented

**LLM Features:**
- **Web-Browsing:** Excluded — all context is local files
- **File I/O:** Included — read module brief, patterns library, config schema; write SKILL.md and data files
- **Sub-Agents:** Excluded — single skill at a time
- **Sub-Processes:** Excluded — linear flow

**Memory:**
- Type: Single-session
- Tracking: None needed (no continuation)

**External Integrations:**
- None required

**Installation Requirements:**
- None — all tools are built-in

---

## Workflow Structure Design

### Step Sequence

| Step | File | Type | Goal | Menu |
|------|------|------|------|------|
| 01 | step-01-select-skill.md | Init (Non-Continuable) | Present 9 skills with descriptions from registry, user selects one | C only |
| 02 | step-02-load-context.md | Middle (Simple) / Auto-proceed | Load module brief sections, patterns library, config schema for selected skill | Auto-proceed |
| 03 | step-03-generate-skill.md | Middle (Standard) | Generate complete SKILL.md content from accumulated context | C only |
| 04 | step-04-bundle-resources.md | Middle (Simple) | Determine and generate data/ files if skill needs runtime reference data | C only |
| 05 | step-05-validate.md | Final | Cross-check triggers vs flow vs instructions, present report, offer "build another?" | None (final) |

### Flow Diagram

```
step-01-select-skill
    │  User picks skill from 9 options
    ▼
step-02-load-context
    │  Auto-loads: module brief sections, patterns lib, config schema
    ▼
step-03-generate-skill
    │  Generates SKILL.md, user confirms before write
    ▼
step-04-bundle-resources
    │  Generates data/ files if needed, user confirms
    ▼
step-05-validate
    │  Runs consistency checks, presents report
    └──→ "Build another?" → back to step-01 OR done
```

### Data Flow

- **step-01** sets `selectedSkill` → stored in output file frontmatter
- **step-02** reads module brief + patterns library + config schema → appends relevant context sections to output file
- **step-03** reads accumulated context from output file → generates SKILL.md content → writes to `skills/{selectedSkill}/SKILL.md`
- **step-04** reads generated SKILL.md → determines what data files are needed → generates to `skills/{selectedSkill}/data/`
- **step-05** reads SKILL.md + data files → validates consistency → appends report to output file

### File Structure

```
build-forge-skill/
├── workflow.md                    # Entry point with frontmatter
├── data/
│   └── skill-registry.md         # 9 skills: name, description, triggers, flow summary, data needs
├── steps-c/
│   ├── step-01-select-skill.md   # Init — skill selection
│   ├── step-02-load-context.md   # Auto-proceed — context loading
│   ├── step-03-generate-skill.md # Middle — SKILL.md generation
│   ├── step-04-bundle-resources.md # Middle — data file generation
│   └── step-05-validate.md       # Final — validation + completion
```

### Output File

**Path:** `{forge_output_folder}/skill-build-{selectedSkill}.md`

**Purpose:** Working document that accumulates context (steps 1-2), tracks generation (steps 3-4), and stores validation report (step 5). The actual deliverables are the SKILL.md and data/ files written to the skills folder.

### Role and Persona

**Agent:** Forge Builder (Morgan)
**Style:** Professional, precise, focused on correctness. Not the forge metaphor personality — Morgan is the module lifecycle manager. Matter-of-fact, technical, thorough.
**Communication:** Direct status updates during autonomous steps, clear prompts during interactive steps.

### Subprocess Optimization

- **step-02 (load-context):** Pattern 3 — subprocess loads module brief (large file), extracts only sections relevant to the selected skill, returns extracted context. Fallback: load and scan in main thread.
- **step-05 (validate):** Pattern 4 — parallel validation checks (triggers consistency, flow completeness, instruction coverage). Each subprocess checks one dimension and returns findings. Fallback: sequential checks in main thread.

### Validation Design

**step-05 checks:**
1. **Structural completeness:** SKILL.md has all required sections (triggers, flow, instructions)
2. **Trigger consistency:** Trigger examples match the skill's purpose from module brief
3. **Flow completeness:** Every trigger has a defined flow path
4. **Instruction coverage:** Instructions cover all flow steps
5. **Data file references:** Any data files referenced in SKILL.md exist in data/
6. **Brief alignment:** Skill definition matches module brief description

### Special Features

- **"Build another?" loop:** After validation in step-05, offer to restart at step-01 for another skill
- **Skill registry data file:** Pre-built reference of all 9 skills with their descriptions, expected triggers, flow summaries, and data requirements — loaded by step-01 for display and by step-02 for context
