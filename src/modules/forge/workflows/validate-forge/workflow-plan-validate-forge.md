---
conversionFrom: 'src/modules/forge/workflows/validate-forge/validate-forge.spec.md'
originalFormat: 'spec.md (workflow specification placeholder)'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-next-step', 'step-10-confirmation', 'step-11-completion']
created: 2026-02-13
completionDate: 2026-02-13
status: COMPLETE
approvedDate: 2026-02-13
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/forge/workflows/validate-forge/validate-forge.spec.md
**Original Format:** Workflow specification document (planning artifact, not yet implemented)
**Detected Structure:** Single spec file defining a 5-step validation workflow for The Forge module

---

## Original Workflow Analysis

### Goal (from source)

Validate The Forge module for internal consistency. Run a comprehensive consistency check across all Forge artifacts — workspace files, skills, reference data, config schema. Ensure everything is aligned and nothing is missing or contradictory before packaging or deployment.

### Original Steps (Complete List)

**Step 1:** Load all artifacts - Collect all workspace files, skills, and reference data
**Step 2:** Structural checks - Verify all required files exist and have correct format
**Step 3:** Coherence checks - Cross-reference skills against patterns library, config schema
**Step 4:** Completeness checks - Ensure all 9 skills are present with required resources
**Step 5:** Generate report - Produce validation report with pass/fail/warnings

### Output / Deliverable

- `{forge_artifacts}/validation-report.md` — Full validation report with findings

### Input Requirements

**Required:**
- All generated workspace files
- All generated skill files
- Reference data files
- module-brief-forge.md (source of truth for completeness)

**Optional:**
- Previous validation report (for delta comparison)

### Key Instructions to LLM

The spec does not contain LLM instruction patterns — it is a planning artifact only. The workflow type is Quality Assurance / Validation, intended to be executed by the Forge Builder agent (Morgan). No other agents involved. The workflow is create-only (steps-c/ only), not tri-modal.

---

## Conversion Notes

**What works well in original:**
- Clear 5-step progression from loading through validation to reporting
- Well-defined inputs and outputs
- Specific validation categories (structural, coherence, completeness)
- Named agent assignment (Forge Builder / Morgan)

**What needs improvement:**
- No actual implementation — spec only, no step files exist
- No detailed validation criteria or rules defined
- No menu structures or user interaction points specified
- Missing specifics on what "correct format" means for structural checks
- No error handling or partial-pass scenarios described

**Compliance gaps identified:**
- No workflow.md entry point file
- No step files (steps-c/) exist
- No frontmatter with BMAD metadata
- No execution rules, sequence enforcement, or state tracking
- No menu handling logic defined
- Needs full BMAD step-file architecture implementation

## Classification Decisions

**Workflow Name:** validate-forge
**Target Path:** src/modules/forge/workflows/validate-forge/

**4 Key Decisions:**
1. **Document Output:** true (produces validation-report.md)
2. **Module Affiliation:** forge (module-based)
3. **Session Type:** single-session
4. **Lifecycle Support:** create-only

**Structure Implications:**
- Only needs `steps-c/` folder (no steps-e/ or steps-v/)
- No continuation logic needed (no step-01b-continue.md)
- Needs output template for validation-report.md
- Standard init step, no continuation detection
- Uses `data/` folder for validation criteria reference data

## Requirements

**Flow Structure:**
- Pattern: linear
- Phases: Init/Load → Structural Validation → Coherence Validation → Completeness Validation → Report Generation
- Estimated steps: 5 (maps 1:1 from spec)

**User Interaction:**
- Style: mostly autonomous
- Decision points: Init only (confirm artifact paths, optionally provide previous report for delta)
- Checkpoint frequency: No mid-workflow checkpoints — runs straight through validation checks and presents final report

**Inputs Required:**
- Required: All generated Forge workspace files, all generated skill files, reference data files, module-brief-forge.md (source of truth)
- Optional: Previous validation report (for delta comparison)
- Prerequisites: Forge module artifacts must already be generated

**Output Specifications:**
- Type: document (validation-report.md)
- Format: structured (defined sections per validation category)
- Sections: Summary, Structural Checks, Coherence Checks, Completeness Checks, Findings, Overall Verdict
- Frequency: single report per run

**Success Criteria:**
- All Forge artifacts loaded and inventoried
- Every structural check produces a pass/fail/warning result
- Cross-references between skills, patterns library, and config schema verified
- All 9 skills confirmed present with required resources
- Final report generated with clear pass/fail verdict and actionable findings

**Instruction Style:**
- Overall: prescriptive
- Notes: Validation criteria must be exact and deterministic. Each check should have a clear pass/fail condition. No creative interpretation — either the artifact meets the criteria or it doesn't.

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** excluded - No creative brainstorming in a validation scan
- **Advanced Elicitation:** excluded - No deep exploration needed, this is pass/fail checking
- **Brainstorming:** excluded - Not applicable to validation workflows

**LLM Features:**
- **Web-Browsing:** excluded - All validation against local artifacts only
- **File I/O:** included - Core requirement: reads all Forge artifacts, writes validation report
- **Sub-Agents:** excluded - Sequential validation, no parallelism needed
- **Sub-Processes:** excluded - Linear single-pass workflow

**Memory:**
- Type: single-session
- Tracking: stepsCompleted in output document frontmatter (for document building, not continuation)

**External Integrations:**
- None required

**Installation Requirements:**
- None — all tools are built-in

## Workflow Design

### File Structure

```
validate-forge/
├── workflow.md                          # Entry point
├── data/
│   └── forge-validation-checklist.md    # Complete validation criteria reference
├── steps-c/
│   ├── step-01-init.md                  # Init: load config, discover artifacts, create report
│   ├── step-02-structural.md            # Structural validation checks
│   ├── step-03-coherence.md             # Coherence validation checks
│   ├── step-04-completeness.md          # Completeness validation checks
│   └── step-05-report.md               # Final: compile verdict, present report
└── templates/
    └── validation-report.template.md    # Structured report template
```

### Step Sequence Design

**Step 1: Init (Non-Continuable, Auto-Proceed)**
- Step type: Init (non-continuable)
- Menu pattern: Auto-proceed (Pattern 3)
- Goal: Load config, resolve `{forge_artifacts}` path, discover all Forge artifacts, create validation-report.md from template
- Subprocess: Pattern 1 — single subprocess to glob/scan all artifact files and return inventory
- Data flow: Creates report file, populates artifact inventory section
- Frontmatter vars: `nextStepFile`, `outputFile`, `reportTemplate`, `forgeArtifactsPath`, `moduleBriefPath`

**Step 2: Structural Validation (Validation Sequence, Auto-Proceed)**
- Step type: Validation sequence
- Menu pattern: Auto-proceed (Pattern 3)
- Goal: Verify all required files exist and have correct format (frontmatter, required sections)
- Subprocess: Pattern 2 — per-file deep analysis for format/frontmatter validation
- Checks:
  - Workspace files exist: SOUL.md, AGENTS.md, IDENTITY.md
  - All 9 skill SKILL.md files exist
  - Each file has valid YAML frontmatter
  - Each file has required sections for its type
  - Reference data files exist (patterns library, config schema)
  - module.yaml valid
- Data flow: Appends structural findings to report
- Frontmatter vars: `nextStepFile`, `outputFile`, `validationChecklist`

**Step 3: Coherence Validation (Validation Sequence, Auto-Proceed)**
- Step type: Validation sequence
- Menu pattern: Auto-proceed (Pattern 3)
- Goal: Cross-reference artifacts for internal consistency
- Subprocess: Pattern 2 — per-skill cross-reference analysis
- Checks:
  - Skills referenced in module-brief match actual skill files
  - Agentic patterns referenced in skills exist in patterns library
  - Config schema references in skills match actual schema fields
  - Agent names consistent across IDENTITY.md, SOUL.md, AGENTS.md
  - Workflow connections in module-brief match actual workflow files
  - Skill trigger examples don't overlap/conflict
- Data flow: Appends coherence findings to report
- Frontmatter vars: `nextStepFile`, `outputFile`, `validationChecklist`

**Step 4: Completeness Validation (Validation Sequence, Auto-Proceed)**
- Step type: Validation sequence
- Menu pattern: Auto-proceed (Pattern 3)
- Goal: Ensure all 9 skills present with required resources
- Subprocess: Pattern 3 — load module-brief, extract expected skills list, compare against actual
- Checks:
  - All 9 skills from module-brief present: design-system, add-agent, recommend-pattern, setup-knowledge, setup-harness, harden-workspace, validate-workspace, export-package, import-package
  - Each skill has required bundled resources
  - All 5 BMAD build workflows present: build-forge-agent, build-forge-skill, update-reference-data, package-forge, validate-forge
  - All agentic patterns documented in patterns library (7 patterns)
  - Knowledge graph plugin files present (if applicable)
  - No orphan files (files that exist but aren't referenced anywhere)
- Data flow: Appends completeness findings to report
- Frontmatter vars: `nextStepFile`, `outputFile`, `validationChecklist`

**Step 5: Report & Verdict (Final Step)**
- Step type: Final step
- Menu pattern: None (final step, no next)
- Goal: Compile all findings into overall verdict, present summary to user
- Logic:
  - Count total checks, passes, failures, warnings
  - Determine overall verdict: PASS (0 failures, 0 warnings), PASS WITH WARNINGS (0 failures, >0 warnings), FAIL (>0 failures)
  - Present executive summary
  - Save completed report
  - Offer to re-run specific validation category if failures found
- Data flow: Updates report header with verdict, marks report complete
- Frontmatter vars: `outputFile`

### Role & Persona

- Role: Quality inspector / validation specialist
- Communication: Direct, factual, no-nonsense. Reports findings objectively.
- Tone: Professional, systematic. Uses check/cross marks for clarity.
- Not collaborative — this is an autonomous scan that reports results.

### Data File: forge-validation-checklist.md

Contains the complete, authoritative checklist of:
- Required workspace files and their expected sections
- Required skill files (all 9) and their expected structure
- Required reference data files
- Cross-reference rules (what must match what)
- Completeness rules (what must exist per module-brief)

This is the single source of truth for all validation criteria. Steps 2-4 load relevant sections from this file.

### Subprocess Optimization Design

| Step | Pattern | What Subprocess Does | Returns |
|------|---------|---------------------|---------|
| Step 1 | Pattern 1 (Glob) | Scan {forge_artifacts} for all files | File inventory with paths, sizes, dates |
| Step 2 | Pattern 2 (Per-file) | Read each file, check frontmatter + sections | Structured findings per file |
| Step 3 | Pattern 2 (Per-skill) | Cross-reference each skill against patterns/config | Coherence findings per skill |
| Step 4 | Pattern 3 (Data) | Load module-brief, extract expected artifacts list | Expected vs actual comparison |

All steps include graceful fallback for LLMs without subprocess capability.
