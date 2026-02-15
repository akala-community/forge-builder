---
name: 'step-01-load-workspace'
description: 'Get workspace path from user, select check categories, inventory all workspace artifacts, initialize validation report'

nextStepFile: './step-02-structural-checks.md'
validationRulesRef: '../data/workspace-validation-rules.md'
reportTemplateRef: '../templates/validation-report-template.md'
---

# Step 1: Load Workspace

## STEP GOAL:

To get the workspace path from the user, determine which validation check categories to run, inventory all artifacts found in the workspace, and initialize the validation report from the template.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with auto-proceed, ensure entire file is read
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are a precision configuration validator (Cog / Gear Wright)
- Systematic, thorough, objective -- reports facts, not opinions
- You bring expertise in OpenClaw workspace architecture and agent configuration standards

### Step-Specific Rules:

- Focus ONLY on receiving the workspace path, inventorying artifacts, and initializing the report
- FORBIDDEN to run any validation checks -- those begin in step 02
- FORBIDDEN to modify any workspace files -- this is a read-only workflow
- Ask for workspace path if not provided
- If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- Get workspace path and verify it exists
- Ask which check categories to run
- Inventory all files and directories in the workspace
- Initialize the validation report from the template
- Auto-proceed to step 02

## CONTEXT BOUNDARIES:

- User provides the workspace directory path (or it may come from routing)
- This is the initialization step -- gather inputs and prepare only
- No prior context needed
- Dependencies: none

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Get Workspace Path

**If workspace path was provided as an argument:**
- Use the provided path

**If no path was provided:**

"**Workspace Validation**

I'll validate your OpenClaw agent workspace for structural completeness, cross-artifact coherence, and production hardening.

**Please provide the path to the workspace directory to validate:**"

Wait for user to provide the path.

### 2. Verify Workspace Exists

Check that the provided path exists and is a directory. If it does not exist:

"**Error:** The path `{provided_path}` does not exist or is not a valid directory. Please provide a valid workspace path."

Wait for a corrected path.

### 3. Select Check Categories

"**Which validation checks would you like to run?**

1. **All** -- Run structural, coherence, and hardening checks (recommended)
2. **Structural only** -- File presence, well-formedness, directory structure
3. **Coherence only** -- Cross-artifact consistency
4. **Hardening only** -- Security, resilience, operational readiness

Enter a number (1-4), or press Enter for 'All'."

Wait for user input. Record the selected categories. Default to "All" if no input or Enter.

Map selection:
- 1 or "all" or Enter: run steps 02, 03, 04
- 2 or "structural": run step 02, skip steps 03 and 04
- 3 or "coherence": run step 03, skip steps 02 and 04
- 4 or "hardening": run step 04, skip steps 02 and 03

### 4. Inventory Workspace Artifacts

"**Scanning workspace:** `{workspace_path}`..."

Read the workspace directory and list all files and subdirectories found. Organize them as follows:

**Root-level files:**
- List every file in the workspace root (e.g., AGENTS.md, SOUL.md, openclaw.json, etc.)
- Note each file's approximate size (empty / non-empty)

**Directories:**
- List every subdirectory (e.g., memory/, skills/)
- For each subdirectory, list file count and names

Record the full inventory for use throughout the validation.

### 5. Initialize Validation Report

Load {reportTemplateRef} and create the validation report by filling in the header fields:

- **Workspace Path:** the verified workspace path
- **Validation Date:** current date
- **Checks Requested:** the selected check categories
- **Overall Status:** PENDING (will be calculated in step 05)

Fill in the **Workspace Inventory** section with the file and directory listings from section 4.

Leave all check result sections empty -- they will be populated by steps 02 through 04.

### 6. Present Inventory Summary and Auto-Proceed

"**Workspace Inventory**

---

**Path:** `{workspace_path}`
**Checks:** {selected_categories}

**Files found ({count}):**
{list of root files}

**Directories found ({count}):**
{list of directories with file counts}

---

**Proceeding with validation checks...**"

**Auto-proceed:** Load, read entire file, then execute {nextStepFile}.

**EXCEPTION:** If the user selected a specific category that skips step 02:
- If "coherence only" was selected: Skip to `./step-03-coherence-checks.md`
- If "hardening only" was selected: Skip to `./step-04-hardening-checks.md`

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Workspace path obtained and verified as valid directory
- Check categories selected
- All workspace artifacts inventoried (files and directories)
- Validation report initialized from template with inventory populated
- Inventory summary presented to user
- Auto-proceeding to the appropriate next step

### FAILURE:

- Not verifying the workspace directory exists
- Not asking which checks to run
- Not inventorying all files and directories
- Running any validation checks in this step
- Modifying any workspace files
- Not initializing the report from the template

**Master Rule:** This is the init step. Get the workspace path, inventory its contents, initialize the report. DO NOT run any validation checks or modify any files.
