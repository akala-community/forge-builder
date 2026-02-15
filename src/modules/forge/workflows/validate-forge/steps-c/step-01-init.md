---
name: 'step-01-init'
description: 'Initialize validation: load config, discover Forge artifacts, create report'

nextStepFile: './step-02-structural.md'
outputFile: '{forge_artifacts}/validation-report.md'
reportTemplate: '../templates/validation-report.template.md'
validationChecklist: '../data/forge-validation-checklist.md'
---

# Step 1: Initialize Validation

## STEP GOAL:

To load module configuration, discover all Forge artifacts at `{forge_artifacts}`, create the validation report from template, and populate the artifact inventory section.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are a quality inspector preparing for a validation scan
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ This is a mostly autonomous step — discover artifacts and report what was found

### Step-Specific Rules:

- 🎯 Focus only on discovering artifacts and creating the report file
- 🚫 FORBIDDEN to run any validation checks yet — that's steps 2-4
- 💬 Use subprocess optimization (Pattern 1) to scan for all artifact files if available
- ⚙️ If subprocess unavailable, perform file discovery in main thread

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Create validation report from {reportTemplate}
- 📖 Populate the Artifact Inventory section with discovered files
- 🚫 FORBIDDEN to proceed without a complete artifact inventory

## CONTEXT BOUNDARIES:

- Available: Module config with `{forge_artifacts}` path
- Focus: File discovery only — no content analysis
- Limits: Do not read file contents, just confirm existence
- Dependencies: None — this is the first step

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Confirm Artifact Location

"**Starting Forge module validation.**

I'll be scanning for artifacts at: `{forge_artifacts}`

Checking that the artifacts directory exists..."

Verify the `{forge_artifacts}` directory exists. If not, report error and halt.

### 2. Discover All Artifacts

Launch a subprocess (or perform in main thread) that scans `{forge_artifacts}` for all files and returns a structured inventory:

**Scan for:**
- Workspace files (SOUL.md, AGENTS.md, IDENTITY.md, etc.)
- Skill directories and SKILL.md files
- Reference data files (patterns library, config schema)
- Workflow files
- Any other files present

**Return:** File paths, file types, and presence status.

### 3. Load Validation Checklist

Load {validationChecklist} to understand what files are expected. Compare discovered files against the expected file list.

### 4. Create Validation Report

Create {outputFile} from {reportTemplate}.

Update the frontmatter:
```yaml
date: '{current date}'
user_name: '{user_name}'
stepsCompleted: ['step-01-init']
lastStep: 'step-01-init'
```

### 5. Populate Artifact Inventory

Append to the **Artifact Inventory** section of {outputFile}:

```markdown
### Files Discovered

| File | Path | Status |
|------|------|--------|
| [file name] | [relative path] | Found / Missing |
...

**Total files discovered:** [count]
**Expected files:** [count from checklist]
**Missing files:** [count]
```

List ALL discovered files and flag any expected files that are missing.

### 6. Present Inventory Summary

"**Artifact inventory complete.**

**Found:** [count] files
**Expected:** [count] files
**Missing:** [count] files

[If missing files]: The following expected files were not found:
- [list missing files]

These will be flagged as failures in subsequent validation steps."

### 7. Present MENU OPTIONS

Display: "**Select:** [C] Continue to Structural Validation"

#### Menu Handling Logic:

- IF C: Save inventory to {outputFile}, update frontmatter, then load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then [Redisplay Menu Options](#7-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and the artifact inventory is saved to {outputFile} will you then load and read fully {nextStepFile} to execute structural validation.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Forge artifacts directory confirmed to exist
- All files discovered and inventoried
- Validation report created from template
- Artifact inventory section populated with file list
- Missing files identified and flagged
- User informed of inventory results

### ❌ SYSTEM FAILURE:

- Not scanning the artifacts directory
- Missing files not flagged
- Validation report not created
- Proceeding without complete inventory
- Running validation checks in this step (too early)

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
