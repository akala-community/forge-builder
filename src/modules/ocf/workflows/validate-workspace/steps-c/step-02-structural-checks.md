---
name: 'step-02-structural-checks'
description: 'Validate file presence, non-emptiness, well-formedness, directory structure, and BOOTSTRAP.md absence'

nextStepFile: './step-03-coherence-checks.md'
validationRulesRef: '../data/workspace-validation-rules.md'
---

# Step 2: Structural Checks

## STEP GOAL:

To verify all required workspace files exist and are well-formed, check expected directories, verify BOOTSTRAP.md is absent, validate openclaw.json presence and format, and append all findings to the validation report.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step, ensure entire file is read
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are a precision configuration validator (Cog / Gear Wright)
- Systematic, thorough, objective -- reports facts, not opinions
- You bring expertise in workspace file structure and OpenClaw conventions

### Step-Specific Rules:

- Focus ONLY on structural validation (file presence, non-emptiness, well-formedness, directory structure)
- FORBIDDEN to run coherence checks -- that comes in step 03
- FORBIDDEN to run hardening checks -- that comes in step 04
- FORBIDDEN to modify any workspace files -- this is a read-only workflow
- Record every check result with PASS, WARNING, or ERROR severity
- If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- Load validation rules for structural checks
- Run all structural checks (S-01 through S-06) against the workspace
- Record each result with severity and detail
- Append findings to the validation report
- Auto-proceed to step 03

## CONTEXT BOUNDARIES:

- Workspace path from step 01
- Workspace file inventory from step 01
- Validation report (initialized) from step 01
- Dependencies: step 01 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Structural Validation Rules

Load {validationRulesRef} and read the **Category 1: Structural Checks** section. Use rules S-01 through S-06 as the check criteria for this step.

### 2. Check Required File Presence (Rule S-01)

Check each of the following required files in the workspace root. Record PASS if found, ERROR if missing.

**Required files:**
- `AGENTS.md`
- `SOUL.md`
- `USER.md`
- `IDENTITY.md`
- `TOOLS.md`
- `HEARTBEAT.md`
- `MEMORY.md`
- `BOOT.md`

For each file, record:
- File name
- Result: PASS or ERROR
- Detail: "Present" or "MISSING - required file not found"

### 3. Check File Non-Emptiness (Rule S-02)

For every file found in the workspace root (from the step 01 inventory), verify it is non-empty (contains more than whitespace).

- Required files that are empty: ERROR with detail "File exists but is empty"
- Optional/other files that are empty: WARNING with detail "File exists but is empty"
- Non-empty files: PASS

### 4. Check File Well-Formedness (Rule S-03)

For every file found that starts with `---` (indicating YAML frontmatter):

- Verify the frontmatter block closes with a second `---`
- If the frontmatter is malformed: WARNING with detail describing the issue
- If the frontmatter is valid: PASS

Files that do not have frontmatter: skip this check (not applicable).

### 5. Check Directory Structure (Rule S-04)

Check for expected directories in the workspace:

- `memory/` directory: WARNING if missing, PASS if present (note file count)
- `skills/` directory: WARNING if missing, PASS if present (note file count)

### 6. Check BOOTSTRAP.md Absence (Rule S-05)

Check whether `BOOTSTRAP.md` exists in the workspace root:

- If ABSENT: PASS with detail "BOOTSTRAP.md correctly absent (bootstrap complete)"
- If PRESENT: WARNING with detail "BOOTSTRAP.md still present -- bootstrap may not be finalized. This file should be deleted after the first bootstrap run."

### 7. Check openclaw.json Presence and Validity (Rule S-06)

Check whether `openclaw.json` exists in the workspace root:

- If ABSENT: WARNING with detail "openclaw.json not found -- configuration file recommended for production use"
- If PRESENT: Read the file and verify it is valid JSON
  - Valid JSON: PASS with detail "openclaw.json present and valid JSON"
  - Invalid JSON: ERROR with detail describing the parse error

### 8. Compile Structural Results

"**Structural Checks Complete**

---

| Rule | Check | Result | Detail |
|------|-------|--------|--------|
{for each check performed: | rule_id | check_description | PASS/WARNING/ERROR | detail |}

**Structural Totals:** {pass_count} PASS / {warning_count} WARNING / {error_count} ERROR

---"

Append these results to the Structural Checks section of the validation report.

### 9. Auto-Proceed

"**Proceeding to coherence checks...**"

**Auto-proceed:** Load, read entire file, then execute {nextStepFile}.

**EXCEPTION:** If the user selected check categories in step 01 that exclude coherence:
- If "structural only" was selected: Skip to `./step-05-report.md`
- If "all" was selected: Proceed to {nextStepFile} as normal

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- All structural validation rules (S-01 through S-06) executed
- Every required file checked for presence
- Every present file checked for non-emptiness
- Frontmatter well-formedness checked where applicable
- Directory structure checked
- BOOTSTRAP.md absence verified
- openclaw.json presence and validity checked
- All results recorded with severity and detail
- Results appended to validation report
- Auto-proceeding to next step

### FAILURE:

- Not checking all required files
- Not checking file non-emptiness
- Skipping frontmatter validation
- Not checking directory structure
- Not checking BOOTSTRAP.md
- Running coherence or hardening checks in this step
- Modifying any workspace files

**Master Rule:** Run all structural checks systematically, record every result, append to report. DO NOT run coherence or hardening checks, and DO NOT modify any files.
