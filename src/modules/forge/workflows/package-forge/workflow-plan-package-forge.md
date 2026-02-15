---
workflowName: package-forge
conversionFrom: 'src/modules/forge/workflows/package-forge/package-forge.spec.md'
originalFormat: 'placeholder-spec'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-next-step', 'step-10-confirmation', 'step-11-completion']
created: 2026-02-13
completionDate: 2026-02-13
status: COMPLETE
approvedDate: 2026-02-13
confirmationType: conversion
coverageStatus: complete
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/forge/workflows/package-forge/package-forge.spec.md
**Original Format:** Placeholder specification document
**Detected Structure:** Single spec document outlining a 6-step build/packaging workflow with defined inputs, outputs, and agent association

---

## Original Workflow Analysis

### Goal (from source)

Bundle The Forge into an installable .ocf.zip package for distribution. Collects all generated workspace files, skills, reference data, and configuration into a single .ocf.zip archive that can be installed into any OpenClaw instance. Injects metadata and generates a setup prompt for first-run configuration.

### Original Steps (Complete List)

**Step 1:** Validate pre-package - Run validate-forge to ensure consistency before packaging
**Step 2:** Collect artifacts - Gather all workspace files, skills, and reference data
**Step 3:** Inject metadata - Add version, build date, compatibility info
**Step 4:** Generate setup prompt - Create first-run setup instructions for the installer
**Step 5:** Bundle .ocf.zip - Create the archive
**Step 6:** Verify package - Test the archive can be extracted and passes basic checks

### Output / Deliverable

- `{forge_artifacts}/forge-{version}.ocf.zip` — Installable package
- `{forge_artifacts}/RELEASE.md` — Release notes (if provided)

### Input Requirements

**Required:**
- All generated workspace files (SOUL.md, AGENTS.md, IDENTITY.md)
- All generated skill files
- Reference data (patterns library, config reference)
- Version number

**Optional:**
- Release notes
- Changelog

### Key Instructions to LLM

- This is a build/packaging workflow — the LLM acts as a build system orchestrator
- Linear, deterministic flow — no branching or user interaction mid-flow
- The workflow should validate before packaging and verify after packaging
- Non-document-producing — output is a zip archive, not a markdown document

---

## Conversion Notes

**What works well in original:**
- Clear, linear 6-step sequence
- Well-defined inputs and outputs
- Pre-validation and post-verification bookends
- Single agent responsibility (Forge Builder / Morgan)

**What needs improvement:**
- No actual implementation — just a spec placeholder
- No step file content — needs full step instructions written
- No error handling or rollback defined
- No .ocf.zip format specification referenced

**Compliance gaps identified:**
- No workflow.md with frontmatter
- No step files (steps-c/ folder)
- No BMAD step structure (STEP GOAL, MANDATORY EXECUTION RULES, etc.)
- No menu handling or continuation logic
- Missing installed_path resolution

---

## Classification Decisions

**Workflow Name:** package-forge
**Target Path:** src/modules/forge/workflows/package-forge/

**4 Key Decisions:**
1. **Document Output:** false (produces .ocf.zip archive, not a document)
2. **Module Affiliation:** forge (part of the forge module)
3. **Session Type:** single-session (linear build process, no multi-session needed)
4. **Lifecycle Support:** create-only (steps-c/ only, no edit/validate modes)

**Structure Implications:**
- Only needs `steps-c/` folder (no steps-e/ or steps-v/)
- No `step-01b-continue.md` needed (single-session)
- No `stepsCompleted` tracking in output (non-document)
- No templates needed (non-document)
- Standard `step-01-init.md` init pattern

---

## Requirements

**Flow Structure:**
- Pattern: linear
- Phases: Init/Validate → Collect → Transform → Bundle → Verify
- Estimated steps: 6 (maps 1:1 from spec)

**User Interaction:**
- Style: mostly autonomous
- Decision points: Step 1 (init) — user confirms version number, input paths, optional release notes
- Checkpoint frequency: init only — rest runs autonomously

**Inputs Required:**
- Required: Generated workspace files (SOUL.md, AGENTS.md, IDENTITY.md), skill files, reference data (patterns library, config reference), version number
- Optional: Release notes, changelog
- Prerequisites: validate-forge must pass (Step 1 runs it)

**Output Specifications:**
- Type: action (creates .ocf.zip archive file)
- Format: Non-document — produces binary archive + optional RELEASE.md
- Output path: `{forge_artifacts}/forge-{version}.ocf.zip`
- Frequency: single (one package per run)

**Success Criteria:**
- validate-forge passes before packaging
- All required artifacts collected and present
- Metadata injected (version, build date, compatibility)
- Setup prompt generated for first-run configuration
- .ocf.zip archive created successfully
- Archive passes extraction and basic verification checks

**Instruction Style:**
- Overall: prescriptive
- Notes: Deterministic build process — exact file operations, no creative facilitation needed. Each step has specific, concrete actions.

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** excluded — deterministic build process, no creative exploration needed
- **Advanced Elicitation:** excluded — inputs are well-defined from spec, no deep discovery needed
- **Brainstorming:** excluded — no ideation in a packaging workflow

**LLM Features:**
- **Web-Browsing:** excluded — no external data needed
- **File I/O:** included — core to workflow (reading workspace files, writing archive, reading/writing metadata)
- **Sub-Agents:** excluded — single linear process, no delegation needed
- **Sub-Processes:** excluded — sequential build steps, no parallelism needed

**Memory:**
- Type: single-session
- Tracking: none (non-document, no state persistence needed)

**External Integrations:**
- None required

**Installation Requirements:**
- None — all tools are built-in LLM capabilities

---

## Workflow Structure Design

### File Structure

```
package-forge/
├── workflow.md                    # Entry point with frontmatter
├── data/
│   └── ocf-format-spec.md         # .ocf.zip format specification
└── steps-c/
    ├── step-01-init.md            # Init: gather version, paths, validate
    ├── step-02-collect.md         # Collect all artifacts
    ├── step-03-metadata.md        # Inject metadata + generate setup prompt
    ├── step-04-bundle.md          # Create .ocf.zip archive
    └── step-05-verify.md          # Verify package + report
```

**Design decision:** Consolidated from 6 spec steps to 5 workflow steps by merging "inject metadata" and "generate setup prompt" (both are transformation steps on collected artifacts, no user interaction between them). This keeps the workflow tight while preserving all functionality.

### Step Sequence Design

**Step 1: Init** (Type: Init Non-Continuable)
- Goal: Gather version number, confirm workspace paths, accept optional release notes/changelog, run validate-forge
- User interaction: User provides version number, confirms input paths, optionally provides release notes
- Menu: Pattern 3 (Auto-proceed after validation passes)
- On validation failure: halt with error, do not proceed
- Frontmatter vars: `nextStepFile`, `forgeWorkspacePath`, `forgeArtifactsPath`

**Step 2: Collect Artifacts** (Type: Middle Simple, Auto-proceed)
- Goal: Scan workspace and collect all files that need to go into the package
- Actions: Read workspace directory, enumerate all workspace files (SOUL.md, AGENTS.md, IDENTITY.md), skill files, reference data files
- Build a manifest of all files to include
- Menu: Pattern 3 (Auto-proceed — deterministic file scan)
- Frontmatter vars: `nextStepFile`, `forgeWorkspacePath`

**Step 3: Metadata + Setup Prompt** (Type: Middle Simple, Auto-proceed)
- Goal: Inject version, build date, compatibility info into package metadata; generate setup prompt for first-run
- Actions: Create manifest.json with metadata, generate SETUP.md with first-run instructions
- Menu: Pattern 3 (Auto-proceed — deterministic transformation)
- Frontmatter vars: `nextStepFile`

**Step 4: Bundle** (Type: Middle Simple, Auto-proceed)
- Goal: Create the .ocf.zip archive containing all collected artifacts + metadata + setup prompt
- Actions: Use file I/O to create zip archive at `{forge_artifacts}/forge-{version}.ocf.zip`
- If release notes provided: also write RELEASE.md
- Menu: Pattern 3 (Auto-proceed)
- Frontmatter vars: `nextStepFile`, `forgeArtifactsPath`

**Step 5: Verify + Complete** (Type: Final Step)
- Goal: Verify the package can be extracted, contents match manifest, report success
- Actions: Extract archive to temp, verify file list, check metadata integrity, report results
- No nextStepFile (final step)
- Present summary with package path, file count, size
- Frontmatter vars: `forgeArtifactsPath`

### Interaction Pattern

```
User invokes workflow
    │
    ▼
Step 1: Init ─── User provides version, confirms paths ─── validate-forge runs
    │                                                            │
    │ (pass)                                              (fail) ├─► HALT with error
    ▼
Step 2: Collect ─── Auto-proceed (scan files, build manifest)
    │
    ▼
Step 3: Metadata ─── Auto-proceed (inject metadata, generate setup prompt)
    │
    ▼
Step 4: Bundle ─── Auto-proceed (create .ocf.zip)
    │
    ▼
Step 5: Verify ─── Auto-proceed (extract, verify, report) ─── DONE
```

### Data Flow

- Step 1 → Step 2: version number, workspace path, optional release notes
- Step 2 → Step 3: file manifest (list of all files to include)
- Step 3 → Step 4: manifest + metadata + setup prompt content
- Step 4 → Step 5: archive path for verification
- All state passed via in-memory context (single-session, no persistence needed)

### Role and Persona

- Role: Build system orchestrator
- Expertise: File operations, packaging, archive creation
- Tone: Technical, precise, status-reporting
- Style: Prescriptive — exact actions, deterministic flow

### Validation and Error Handling

- Step 1: validate-forge must pass; halt on failure
- Step 2: All required files must exist; report missing files
- Step 4: Archive creation must succeed; report on failure
- Step 5: Extraction verification must match manifest; report discrepancies

### Data File: ocf-format-spec.md

Will contain:
- .ocf.zip directory structure specification
- Required files (manifest.json, SETUP.md)
- Metadata schema (version, buildDate, compatibility, fileCount)
- File organization within the archive
