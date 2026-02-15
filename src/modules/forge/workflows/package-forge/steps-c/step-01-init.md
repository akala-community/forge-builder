---
name: 'step-01-init'
description: 'Initialize packaging — gather version, confirm workspace, run validation'

nextStepFile: './step-02-collect.md'
forgeWorkspacePath: '{forge_artifacts}'
ocfFormatSpec: '../data/ocf-format-spec.md'
---

# Step 1: Initialize Package Build

## STEP GOAL:

Gather the version number, confirm the Forge workspace location and required files, accept optional release notes, and run validate-forge to ensure workspace consistency before packaging.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a build system orchestrator packaging The Forge for distribution
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ You bring packaging expertise and systematic file operations
- ✅ User brings their Forge workspace and version requirements

### Step-Specific Rules:

- 🎯 Focus only on gathering inputs and validating workspace
- 🚫 FORBIDDEN to start collecting or packaging files yet
- 💬 Be precise — this is a build pipeline, not a creative session

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Gather all inputs needed for subsequent steps
- 📖 Validate workspace before proceeding
- 🚫 HALT on validation failure — do not proceed to packaging

## CONTEXT BOUNDARIES:

- Available: Forge module config with `forge_artifacts` path
- Focus: Version number, workspace validation, optional release notes
- Limits: Do not read or collect individual files yet
- Dependencies: None — this is the first step

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Format Specification

Load `{ocfFormatSpec}` to understand the .ocf.zip archive structure and required files.

### 2. Gather Version Number

"**Package Forge — Build Pipeline**

**Step 1: Initialize**

I need a few things before we start packaging:

**Version number** (semver format, e.g., 1.0.0):"

Wait for user to provide version number. Validate it follows semver format (MAJOR.MINOR.PATCH).

### 3. Confirm Workspace Location

"**Workspace location:** `{forgeWorkspacePath}`

Let me verify this directory exists and contains the required files..."

Scan `{forgeWorkspacePath}` for:
- SOUL.md (required)
- AGENTS.md (required)
- IDENTITY.md (required)
- Skill files
- Reference data (patterns, config)

Report what was found:

"**Workspace scan results:**
- [x] SOUL.md — found
- [x] AGENTS.md — found
- [x] IDENTITY.md — found
- Skills: {count} files found
- Reference data: {count} files found

**Total files to package:** {count}"

If any required files are missing, report and HALT:

"**ERROR: Missing required files:** {list}
Cannot proceed with packaging. Please ensure all required files are present."

### 4. Optional Inputs

"**Optional inputs:**
- **Release notes?** Provide text or path to a file, or skip
- **Changelog?** Provide text or path to a file, or skip"

Accept user input. If skipped, note that RELEASE.md will not be included.

### 5. Run Validation

"**Running pre-package validation...**"

Check for:
1. All required workspace files exist and are non-empty
2. No obvious formatting issues (valid markdown)
3. No broken internal references between workspace files

Report results:

"**Validation results:**
- {count} checks passed
- {count} warnings
- {count} errors

**Status:** {PASS/FAIL}"

If FAIL: HALT and report errors. Do not proceed.
If PASS: Continue.

### 6. Confirm and Proceed

"**Build configuration:**
- **Version:** {version}
- **Workspace:** {forgeWorkspacePath}
- **Files to package:** {count}
- **Release notes:** {yes/no}
- **Validation:** PASSED

**Proceeding to artifact collection...**"

#### Menu Handling Logic:

- After validation passes and configuration is confirmed, immediately load, read entire file, then execute {nextStepFile}

#### EXECUTION RULES:

- This is an auto-proceed step after validation passes
- HALT on validation failure — do not proceed

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN validation passes and configuration is confirmed will you load and read fully `{nextStepFile}` to begin artifact collection.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Version number gathered and validated
- Workspace scanned and all required files found
- Optional inputs collected or skipped
- Validation passed
- Build configuration confirmed
- Proceeding to step 2

### ❌ SYSTEM FAILURE:

- Proceeding without version number
- Skipping workspace scan
- Proceeding after validation failure
- Not reporting missing required files
- Starting to collect/package files in this step

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
