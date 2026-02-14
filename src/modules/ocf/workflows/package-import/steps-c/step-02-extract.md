---
name: 'step-02-extract'
description: 'Unpack workspace files from the archive to target directories'

nextStepFile: './step-03-configure.md'
installationChecklist: '../data/installation-checklist.md'
reportOutput: '{reportOutput}'
---

# Step 2: Extract Package

## STEP GOAL:

To unpack workspace files from the .ocf.zip archive to the target workspace directory, verify the extraction produced a valid workspace structure, and record the results.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 DO NOT BE LAZY - VERIFY EVERY EXTRACTED FILE
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- ✅ Extraction does NOT stop for user input unless conflicts detected - auto-proceed
- ⚙️ If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are the **Installation Specialist** — precise, systematic extraction
- ✅ Verify EVERY file after extraction

### Step-Specific Rules:

- 🎯 Focus ONLY on extraction and verification
- 🚫 FORBIDDEN to merge configuration — that's step 03
- 🚫 FORBIDDEN to register agents — that's step 04
- 💬 Report findings as [PASS], [FAIL], or [WARN] per check

## EXECUTION PROTOCOLS:

- 🎯 Extract archive contents to target directory
- 💾 Append extraction results to {reportOutput}
- 📖 Save report before loading next step
- 🚫 DO NOT halt for user input unless workspace conflicts detected

## CONTEXT BOUNDARIES:

- Package validation from step 01 confirmed archive and setup prompt are valid
- Target workspace directory is known from setup.md parsing
- Focus ONLY on extracting files and verifying structure
- Dependencies: step 01 must be complete (package validated, report initialized)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Extraction Checks

Load {installationChecklist} and focus on the "## Extraction Checks" section.

### 2. Prepare Target Directory

**Check if target workspace directory exists:**

**If directory exists and contains workspace files:**
- List existing files
- [WARN] "Target directory already contains workspace files"
- Present to user: "The target directory `{target_workspace}` already contains files. Should I proceed? Existing files with the same name will be overwritten."
- Wait for confirmation

**If directory does not exist:**
- Create the target workspace directory
- [PASS] "Target directory created"

### 3. Extract Archive Contents

"**Extracting package contents...**"

Extract the .ocf.zip archive to the target workspace directory.

List all extracted files and directories.

### 4. Verify Extraction

For each extraction check in the checklist:

**Target directory accessible:**
- Check: target directory exists and is writable
- Record: [PASS] or [FAIL]

**Required workspace files present:**
- Check: SOUL.md exists in extracted files
- Check: AGENTS.md exists in extracted files
- Record: [PASS] or [FAIL] for each

**Directory structure valid:**
- Check: standard directories present (memory/, skills/, etc.)
- Record: [PASS] or [WARN] with details

### 5. Inventory Extracted Files

List ALL files extracted:

```
Root files: {count}
- SOUL.md
- AGENTS.md
- USER.md
- IDENTITY.md
- [etc.]

Directories: {count}
- memory/ ({file_count} files)
- skills/ ({file_count} files)
- [etc.]

Configuration fragments:
- openclaw.json fragment: {found/not found}
```

### 6. Append Findings to Report

Replace the "## Extraction Summary" section in {reportOutput} with actual findings:

```markdown
## Extraction Summary

**Target Directory:** {target_workspace}
**Files Extracted:** {count}

### Extracted Files
| File/Directory | Type | Status |
|----------------|------|--------|
| SOUL.md | Required | [PASS/FAIL] |
| AGENTS.md | Required | [PASS/FAIL] |
| USER.md | Optional | [PASS/WARN] |
| IDENTITY.md | Optional | [PASS/WARN] |
| memory/ | Directory | [PASS/WARN] |
| skills/ | Directory | [PASS/WARN] |

### Extraction Checks
| Check | Status | Details |
|-------|--------|---------|
| Target accessible | [PASS/FAIL] | {details} |
| Required files present | [PASS/FAIL] | {details} |
| Structure valid | [PASS/WARN] | {details} |

**Extraction Summary:** {pass_count} passed, {fail_count} failed, {warn_count} warnings
```

### 7. Save Report and Auto-Proceed

"**Extraction complete.** {pass_count} passed, {fail_count} failed, {warn_count} warnings. Proceeding to configuration merge..."

Save the report, then immediately load, read entire file, then execute {nextStepFile}.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Archive extracted to target directory
- All extracted files inventoried
- Required files verified (SOUL.md, AGENTS.md)
- Structure validated
- Findings appended to report
- Report saved before proceeding
- Auto-proceeded to next step

### ❌ SYSTEM FAILURE:

- Not verifying extraction completed
- Skipping required file checks
- Not inventorying all extracted files
- Not saving report before proceeding
- Halting when should auto-proceed (unless critical failure)

**Master Rule:** Extract everything, verify everything, document everything. Auto-proceed unless critical failure.
