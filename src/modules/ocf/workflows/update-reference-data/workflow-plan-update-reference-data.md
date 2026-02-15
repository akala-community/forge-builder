---
conversionFrom: 'src/modules/forge/workflows/update-reference-data/update-reference-data.spec.md'
originalFormat: 'BMAD workflow spec (placeholder)'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-next-step', 'step-10-confirmation', 'step-11-completion']
created: 2026-02-13
completionDate: 2026-02-13
status: COMPLETE
approvedDate: 2026-02-13
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/forge/workflows/update-reference-data/update-reference-data.spec.md
**Original Format:** BMAD workflow specification (placeholder - not yet implemented)
**Detected Structure:** Single specification document describing a 6-step maintenance/data-refresh workflow for The Forge module

---

## Original Workflow Analysis

### Goal (from source)

Refresh the agentic patterns library and OpenClaw config reference against the current OpenClaw source code. Scans the OpenClaw source code to extract current configuration schema, available features, and platform capabilities. Updates The Forge's reference data so that generated configs are always valid against the latest OpenClaw version.

### Original Steps (Complete List)

**Step 1:** Locate OpenClaw source - Find and validate the OpenClaw source tree
**Step 2:** Extract config schema - Parse openclaw.json schema, bindings, model config
**Step 3:** Extract platform features - Identify available hooks, spawn config, memory backends
**Step 4:** Update pattern library - Refresh agentic pattern implementations with current features
**Step 5:** Update config reference - Write updated config reference data
**Step 6:** Validate references - Cross-check updated data for accuracy

### Output / Deliverable

- `data/patterns/` — Updated agentic pattern library
- `data/config-reference/` — Updated OpenClaw config schema reference
- Document-producing workflow

### Input Requirements

**Required:**
- Path to OpenClaw source code
- Current pattern library files
- Current config reference files

**Optional:**
- Specific sections to update (partial refresh)

### Key Instructions to LLM

The spec does not define LLM instruction patterns — it is a placeholder spec indicating "Use the create-workflow workflow to build this workflow." The workflow is intended to be executed by the Forge Builder (Morgan) agent. No other agents are involved. The workflow is create-only (steps-c/ only, no tri-modal structure).

---

## Conversion Notes

**What works well in original:**
- Clear 6-step progression from source discovery through validation
- Well-defined inputs and outputs
- Logical flow: locate → extract → update → validate

**What needs improvement:**
- No actual step files exist — this is purely a specification
- No LLM instruction patterns defined
- No menu structures, execution protocols, or completion criteria
- No templates for output data formats
- No details on HOW to parse config schema or extract features

**Compliance gaps identified:**
- No workflow.md entry point file
- No step files (steps-c/ directory missing)
- No frontmatter with proper BMAD metadata
- No execution rules, sequence enforcement, or state tracking
- No data templates or reference file formats defined
- Missing installed_path resolution — spec references `{project-root}/_bmad/forge/workflows/update-reference-data`

---

## Classification Decisions

**Workflow Name:** update-reference-data
**Target Path:** _bmad/forge/workflows/update-reference-data/

**4 Key Decisions:**
1. **Document Output:** true (produces pattern library and config reference files)
2. **Module Affiliation:** Module-based: Forge (custom module)
3. **Session Type:** Single-session (systematic extraction, not creative dialogue)
4. **Lifecycle Support:** Create-only (maintenance workflow, no edit/validate needed)

**Structure Implications:**
- Only needs `steps-c/` directory (no steps-e/ or steps-v/)
- No `step-01b-continue.md` needed (single-session)
- Standard init step (no continuation logic)
- Output files are data references, not a single document — multiple output files in `data/` subdirectories
- Module-based so has access to Forge module variables

---

## Requirements

**Flow Structure:**
- Pattern: Linear (locate → extract → extract → update → update → validate)
- Phases: Source Discovery, Schema Extraction, Feature Extraction, Data Update, Validation
- Estimated steps: 6 step files (matching the spec's 6-step plan)

**User Interaction:**
- Style: Mostly autonomous with checkpoint at init (source path confirmation)
- Decision points: Step 1 (confirm source path), Step 4-5 (confirm before overwriting existing data)
- Checkpoint frequency: Minimal — this is a maintenance task, not creative work

**Inputs Required:**
- Required: Path to OpenClaw source code (or auto-detect from current project)
- Required: Current pattern library files (existing data/ directory in workflow)
- Required: Current config reference files (existing data/ directory in workflow)
- Optional: Specific sections to update (partial refresh mode)
- Prerequisites: OpenClaw source code must be accessible and contain expected structure

**Output Specifications:**
- Type: Multiple data reference documents (not a single document)
- Format: Structured — specific schema for patterns and config reference
- Output pattern: Plan-then-Build — steps 1-3 gather data into a plan/extraction document, steps 4-5 write final reference files, step 6 validates
- Files produced:
  - `data/patterns/*.md` — Individual agentic pattern reference files
  - `data/config-reference/*.md` — Config schema reference files
  - Extraction report (intermediate, used by update steps)

**Success Criteria:**
- All config schema entries from OpenClaw source are captured in config reference
- All platform features (hooks, spawn config, memory backends) are documented
- Pattern library reflects current OpenClaw capabilities
- No stale references to removed features
- Cross-validation passes: every referenced feature exists in source

**Instruction Style:**
- Overall: Prescriptive — this is systematic extraction, not creative work
- Notes: Steps should use exact file patterns and parsing instructions; the LLM needs to know WHERE to look in OpenClaw source and WHAT to extract. Each step should include specific glob patterns, file names, and data structures to target.

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** Excluded — maintenance/extraction task, no creative brainstorming needed
- **Advanced Elicitation:** Excluded — systematic extraction, not exploratory discovery
- **Brainstorming:** Excluded — no ideation required

**LLM Features:**
- **Web-Browsing:** Excluded — all data sourced from local OpenClaw source code
- **File I/O:** Included — critical for reading OpenClaw source files and writing reference data
- **Sub-Agents:** Excluded — linear sequential task, no parallel specialization needed
- **Sub-Processes:** Excluded — steps are sequential and dependent on prior extractions

**Memory:**
- Type: Single-session
- Tracking: Minimal — no stepsCompleted needed, workflow runs start to finish

**External Integrations:**
- None required

**Installation Requirements:**
- None — all tools are built-in LLM features (file I/O)

---

## Workflow Structure Design

### File Structure

```
update-reference-data/
├── workflow.md                          # Entry point
├── steps-c/
│   ├── step-01-init.md                  # Locate & validate OpenClaw source
│   ├── step-02-extract-config.md        # Extract config schema
│   ├── step-03-extract-features.md      # Extract platform features
│   ├── step-04-update-patterns.md       # Update pattern library files
│   ├── step-05-update-config-ref.md     # Update config reference files
│   └── step-06-validate.md              # Cross-validate all references
├── data/
│   └── extraction-targets.md            # What to look for in OpenClaw source
└── templates/
    ├── extraction-report.md             # Intermediate extraction document template
    ├── pattern-entry.md                 # Template for individual pattern entries
    └── config-reference-entry.md        # Template for config reference entries
```

### Step-by-Step Design

#### Step 1: Init — Locate & Validate OpenClaw Source
- **Type:** Init (Non-Continuable)
- **Menu:** Auto-proceed (Pattern 3)
- **Goal:** Find the OpenClaw source tree, validate it has expected structure
- **Sequence:**
  1. Ask user for OpenClaw source path (or auto-detect from project root)
  2. Validate source tree: check for key directories/files (src/, packages/, CLAUDE.md, package.json)
  3. List discovered source structure summary
  4. Create extraction report from template (intermediate document)
  5. Auto-proceed to step 2
- **Output:** Creates extraction report file from template
- **Subprocess:** None needed — just file existence checks
- **Frontmatter vars:** `nextStepFile`, `extractionReportTemplate`, `extractionReportFile`

#### Step 2: Extract Config Schema
- **Type:** Middle (Simple)
- **Menu:** C only (Pattern 2) — confirm extraction results before proceeding
- **Goal:** Parse OpenClaw config schema, model config, bindings
- **Sequence:**
  1. Load `data/extraction-targets.md` for config schema targets
  2. Read OpenClaw source files for config schema (e.g., types, JSON schemas, config interfaces)
  3. Extract: all config keys, their types, defaults, descriptions, validation rules
  4. Extract: model config options (providers, models, parameters)
  5. Extract: binding/integration config (MCP servers, hooks, permissions)
  6. Append extracted config schema to extraction report
  7. Present summary of what was found, ask user to confirm [C]
- **Output:** Appends to extraction report
- **Subprocess:** Pattern 2 — per-file deep analysis of source files, return structured findings
- **Frontmatter vars:** `nextStepFile`, `extractionReportFile`, `extractionTargetsData`

#### Step 3: Extract Platform Features
- **Type:** Middle (Simple)
- **Menu:** C only (Pattern 2)
- **Goal:** Identify available hooks, spawn config, memory backends, and other platform capabilities
- **Sequence:**
  1. Load extraction targets for platform features
  2. Read OpenClaw source for: hook definitions, spawn configuration, memory backends
  3. Extract: available hook types and their signatures
  4. Extract: spawn/subprocess configuration options
  5. Extract: memory/state management backends
  6. Extract: any other platform features (permissions, auth, etc.)
  7. Append extracted features to extraction report
  8. Present summary, ask user to confirm [C]
- **Output:** Appends to extraction report
- **Subprocess:** Pattern 2 — per-file analysis
- **Frontmatter vars:** `nextStepFile`, `extractionReportFile`, `extractionTargetsData`

#### Step 4: Update Pattern Library
- **Type:** Middle (Simple)
- **Menu:** C only (Pattern 2)
- **Goal:** Refresh agentic pattern reference files based on extracted data
- **Sequence:**
  1. Load current pattern library files (existing data/patterns/ if any)
  2. Load extraction report (config + features)
  3. For each pattern category: compare current vs extracted, identify additions/removals/changes
  4. Generate updated pattern reference files using template
  5. Write updated files to output location
  6. Present diff summary (added/removed/changed), ask user to confirm [C]
- **Output:** Updated pattern library files
- **Subprocess:** Pattern 2 — per-pattern analysis and generation
- **Frontmatter vars:** `nextStepFile`, `extractionReportFile`, `patternEntryTemplate`, `patternOutputDir`

#### Step 5: Update Config Reference
- **Type:** Middle (Simple)
- **Menu:** C only (Pattern 2)
- **Goal:** Write updated config reference data files
- **Sequence:**
  1. Load current config reference files (existing data/config-reference/ if any)
  2. Load extraction report (config schema section)
  3. For each config category: compare current vs extracted, identify changes
  4. Generate updated config reference files using template
  5. Write updated files to output location
  6. Present diff summary, ask user to confirm [C]
- **Output:** Updated config reference files
- **Subprocess:** Pattern 2 — per-config-section analysis
- **Frontmatter vars:** `nextStepFile`, `extractionReportFile`, `configRefEntryTemplate`, `configRefOutputDir`

#### Step 6: Validate References
- **Type:** Final Step (Validation Sequence + Final)
- **Menu:** None (auto-complete)
- **Goal:** Cross-check all updated data against source for accuracy
- **Sequence:**
  1. Load all updated pattern files
  2. Load all updated config reference files
  3. Cross-validate: every referenced feature exists in OpenClaw source
  4. Cross-validate: no stale references to removed features
  5. Cross-validate: config schema entries match source definitions
  6. Generate validation report (pass/fail per check)
  7. Present final summary with validation results
  8. Mark workflow complete
- **Output:** Validation report appended to extraction report, workflow marked complete
- **Subprocess:** Pattern 1 — grep across all output files for referenced features, check against source
- **Frontmatter vars:** `extractionReportFile`, `patternOutputDir`, `configRefOutputDir`

### Data Flow

```
OpenClaw Source ──→ [Step 1: Locate] ──→ Source path validated
                                         │
                                         ▼
                   [Step 2: Config] ──→ Extraction Report (config section)
                                         │
                                         ▼
                   [Step 3: Features] ──→ Extraction Report (features section)
                                         │
                    ┌────────────────────┤
                    ▼                    ▼
      [Step 4: Patterns]      [Step 5: Config Ref]
           │                        │
           ▼                        ▼
    data/patterns/*.md     data/config-reference/*.md
           │                        │
           └───────────┬────────────┘
                       ▼
              [Step 6: Validate]
                       │
                       ▼
              Validation Report
```

### Interaction Patterns

- **Step 1:** User provides source path, or auto-detect. Auto-proceed after validation.
- **Steps 2-5:** Autonomous extraction/generation with C-only confirmation checkpoint between each.
- **Step 6:** Fully autonomous validation, presents final results.

### Role and Persona

- **Role:** Forge Builder (Morgan) — systematic, methodical, precise
- **Communication:** Direct and technical. Report findings concisely. No creative flourishes.
- **Tone:** Professional maintenance worker. "Scanning source... Found 47 config entries. Extracting..."

### Subprocess Optimization

- **Steps 2-3:** Pattern 2 (per-file deep analysis) — each source file analyzed independently, return structured extraction findings
- **Steps 4-5:** Pattern 2 (per-pattern/per-config generation) — each output file generated independently
- **Step 6:** Pattern 1 (grep/regex validation) — single subprocess scans all output files for references, validates against source
- **All steps:** Include graceful fallback for LLMs without subprocess capability
