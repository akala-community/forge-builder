---
name: 'step-02-validate-package'
description: 'Validate package structure, verify expected files, check for conflicts with existing workspace'

nextStepFile: './step-03-install-files.md'
packageStructureRef: '../data/package-structure-reference.md'
---

# Step 2: Validate Package

## STEP GOAL:

To validate the extracted package structure against the expected OCF package format, verify all expected files are present and well-formed, check for conflicts with any existing files in the target workspace, and report issues before proceeding to installation.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step, ensure entire file is read
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are an installation specialist (Cog / Gear Wright)
- Systematic, precise, methodical
- You bring expertise in workspace validation and conflict detection

### Step-Specific Rules:

- Focus ONLY on validation and conflict detection
- FORBIDDEN to install any files yet - that comes in step 03
- FORBIDDEN to merge configuration - that comes in step 04
- Report all issues clearly with severity levels
- If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- Validate package structure against expected format
- Verify all expected files are present and non-empty
- Check target workspace for existing files that would conflict
- Compile a validation report
- Auto-proceed if no blocking issues; pause if blocking issues found

## CONTEXT BOUNDARIES:

- Extracted package contents from step 01
- Target workspace path from step 01
- Package metadata (system name, OCF version) from step 01
- Dependencies: step 01 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Package Structure Reference

Load {packageStructureRef} to understand the expected package format.

### 2. Validate Package Structure

Check the extracted package contents against the expected structure.

**Required workspace files (ERROR if missing):**
- AGENTS.md
- SOUL.md
- USER.md

**Expected workspace files (WARNING if missing):**
- IDENTITY.md
- TOOLS.md
- HEARTBEAT.md
- MEMORY.md
- BOOT.md
- openclaw.json

**Expected directories (WARNING if missing):**
- skills/
- memory/

For each file present, verify it is non-empty and readable.

Record the result for each check: PASS, WARNING, or ERROR.

### 3. Validate OCF Metadata

Verify OCF metadata is present and well-formed:

1. Check that the setup prompt (*.setup.md) has valid YAML frontmatter with required fields
2. Check that AGENTS.md has OCF metadata in its frontmatter (ocf_version, ocf_system_name)
3. If metadata fields are missing, record as WARNING (not blocking)

### 4. Check for Target Conflicts

Examine the target workspace directory for existing files that would be overwritten:

"**Checking target workspace for conflicts...**"

For each file in the package, check if a file with the same name already exists at the target path:

**Conflict categories:**
- **Root files** (AGENTS.md, SOUL.md, etc.) - check target root
- **Skills** (skills/*.md) - check target skills/ directory
- **Memory** (memory/*) - check target memory/ directory
- **Config** (openclaw.json) - check target root

Record each conflict found with the file path.

### 5. Compile Validation Report

"**Package Validation Report**

---

**Structure Validation:**
{for each check: file/dir name - PASS/WARNING/ERROR with detail}

**Metadata Validation:**
- Setup prompt: {present/missing}
- OCF version stamp: {present/missing}
- System name: {present/missing}

**Conflict Detection:**
{count} conflict(s) found with existing workspace files:
{list each conflicting file, or 'No conflicts detected'}

**Overall Status:** {PASS / PASS WITH WARNINGS / BLOCKED}

---"

### 6. Handle Results

**IF no errors and no conflicts (PASS):**

"**Validation passed.** No issues detected. Proceeding to file installation..."

Auto-proceed: Load, read entire file, then execute {nextStepFile}.

**IF warnings only but no errors and no conflicts (PASS WITH WARNINGS):**

"**Validation passed with warnings.** The package is missing some expected files but has all required files. Proceeding to file installation..."

Auto-proceed: Load, read entire file, then execute {nextStepFile}.

**IF conflicts detected (regardless of other status):**

"**Conflicts detected.** The following files already exist in the target workspace and will need to be handled during installation:

{list each conflict}

Conflict resolution options will be presented during the installation step (overwrite, skip, or merge where applicable).

**Select:** [C] Continue to installation (handle conflicts in next step)"

Wait for user input.

- IF C: Load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then redisplay menu

**IF blocking errors found (BLOCKED):**

"**Validation failed.** The package has critical issues:

{list each error}

The package cannot be installed in its current state. Please check the package source and re-export if needed.

**Select:** [R] Retry with a different package | [F] Force proceed anyway"

Wait for user input.

- IF R: Return to step 01 (reload step-01-receive-package.md)
- IF F: Note forced status and load, read entire file, then execute {nextStepFile}

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Package structure validated against expected format
- All files checked for presence and readability
- OCF metadata validated
- Target workspace checked for conflicts
- Validation report presented with clear status
- Appropriate action taken based on results (auto-proceed or pause)

### FAILURE:

- Not checking all expected files
- Not detecting conflicts with existing workspace
- Installing files during validation
- Not reporting validation results clearly
- Auto-proceeding when blocking errors exist

**Master Rule:** Validate thoroughly, report clearly, auto-proceed if clean. DO NOT install any files in this step.
