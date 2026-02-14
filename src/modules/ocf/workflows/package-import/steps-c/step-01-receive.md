---
name: 'step-01-receive'
description: 'Accept and validate the .ocf.zip archive and setup.md prompt'

nextStepFile: './step-02-extract.md'
installationChecklist: '../data/installation-checklist.md'
reportTemplate: '../templates/installation-report-template.md'
reportOutput: '{bmb_creations_output_folder}/ocf/installation-report-{current_date}.md'
---

# Step 1: Receive and Validate Package

## STEP GOAL:

To accept the .ocf.zip archive path and setup.md path from the user, validate both exist and are well-formed, and initialize the installation report.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are an installation specialist (Cog / Gear Wright)
- ✅ Systematic, precise, methodical
- ✅ You bring package management and workspace architecture expertise

### Step-Specific Rules:

- 🎯 Focus ONLY on receiving and validating inputs
- 🚫 FORBIDDEN to extract or install anything yet — that comes in steps 02-04
- 💬 Ask for paths if not provided as arguments
- ⚙️ If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- 🎯 Get archive and setup prompt paths, verify they exist
- 💾 Create installation report from template
- 📖 Parse setup.md for installation instructions
- 🚫 DO NOT extract or modify any files yet

## CONTEXT BOUNDARIES:

- User provides .ocf.zip path and setup.md path (or they may come from arguments)
- This is the initialization step — gather and validate inputs only
- No prior context needed
- Dependencies: none

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Get Package Paths

**If paths were provided as arguments:**
- Use the provided archive path and setup.md path

**If no paths were provided:**

"**Package Import**

I'll help you install an OCF package on your OpenClaw instance.

**Please provide the path to the .ocf.zip archive:**"

Wait for user to provide the archive path.

"**Please provide the path to the setup.md prompt:**

This is the companion setup file that came with the archive."

Wait for user to provide the setup prompt path.

### 2. Validate Archive Exists

Check that the .ocf.zip file exists at the provided path.

**If it doesn't exist:**
"**Error:** The archive `{provided_path}` does not exist. Please provide a valid path to the .ocf.zip file."

**If it exists:**
Record the archive path.

### 3. Validate Setup Prompt Exists

Check that the setup.md file exists at the provided path.

**If it doesn't exist:**
"**Error:** The setup prompt `{provided_path}` does not exist. Please provide a valid path to the setup.md file."

**If it exists:**
Read the setup.md file completely.

### 4. Parse Setup Prompt

Read the setup.md file and extract:
- Agent system name
- Target workspace directory (if specified)
- Installation instructions
- Any configuration fragments or overlays
- Any special requirements

Record the parsed information.

### 5. Load Installation Checklist

Load {installationChecklist} and focus on the "## Package Validation" section.

Run all package validation checks:
- Archive exists: [PASS/FAIL]
- Archive is valid zip: [PASS/FAIL]
- Setup prompt exists: [PASS/FAIL]
- Setup prompt is non-empty: [PASS/FAIL]

If any FAIL: report the failure and halt.

### 6. Create Installation Report

Load {reportTemplate} and create the installation report at {reportOutput}.

Replace template placeholders:
- `{current_date}` -> today's date
- `{package_path}` -> the archive path
- `{setup_prompt_path}` -> the setup prompt path
- `{target_workspace}` -> the target workspace from setup.md

Replace the "## Package Info" section with actual information:

```markdown
## Package Info

**Archive:** {archive_path}
**Setup Prompt:** {setup_prompt_path}
**Agent System Name:** {system_name from setup.md}
**Target Workspace:** {target_workspace}

### Package Validation
| Check | Status | Details |
|-------|--------|---------|
| Archive exists | [PASS/FAIL] | {details} |
| Valid zip | [PASS/FAIL] | {details} |
| Setup prompt exists | [PASS/FAIL] | {details} |
| Setup prompt non-empty | [PASS/FAIL] | {details} |

**Validation Summary:** {pass_count} passed, {fail_count} failed
```

### 7. Present Summary and Auto-Proceed

"**Package received and validated.**

**Archive:** `{archive_path}`
**System Name:** {system_name}
**Target:** `{target_workspace}`
**Validation:** {pass_count} passed, {fail_count} failed

**Proceeding to extraction...**"

Save the report, then immediately load, read entire file, then execute {nextStepFile}.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Archive path obtained and verified
- Setup prompt path obtained and verified
- Setup prompt parsed for installation instructions
- All package validation checks run
- Installation report initialized
- Auto-proceeding to extraction

### ❌ SYSTEM FAILURE:

- Not verifying archive exists
- Not reading setup.md completely
- Starting extraction before validation
- Not creating the installation report
- Halting when should auto-proceed (unless validation fails)

**Master Rule:** This is the init step. Get inputs, validate, initialize report, then auto-proceed. DO NOT extract or install anything.
