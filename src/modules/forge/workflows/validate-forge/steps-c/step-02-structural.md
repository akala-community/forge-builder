---
name: 'step-02-structural'
description: 'Run structural validation checks on all Forge artifacts'

nextStepFile: './step-03-coherence.md'
outputFile: '{forge_artifacts}/validation-report.md'
validationChecklist: '../data/forge-validation-checklist.md'
---

# Step 2: Structural Validation

## STEP GOAL:

To verify all required Forge files exist and have correct format — valid YAML frontmatter, required sections for their type, and proper file structure.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are a quality inspector running structural checks
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ This is an autonomous validation step — run checks and record findings

### Step-Specific Rules:

- 🎯 Focus only on structural checks — file existence, format, frontmatter, required sections
- 🚫 FORBIDDEN to check cross-references or coherence — that's step 3
- 🚫 FORBIDDEN to check completeness counts — that's step 4
- 💬 Use subprocess optimization (Pattern 2) for per-file deep analysis if available
- ⚙️ If subprocess unavailable, perform analysis in main thread

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append all findings to the Structural Validation section of {outputFile}
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to proceed without completing all structural checks

## CONTEXT BOUNDARIES:

- Available: Artifact inventory from Step 1 in {outputFile}
- Focus: File structure only — does each file have the right shape?
- Limits: Do not evaluate content quality or cross-references
- Dependencies: Step 1 must be complete (artifact inventory populated)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Validation Criteria

Load {validationChecklist} and extract the **Structural Checks** section. This defines what files are expected and what sections each file type must contain.

### 2. Check Workspace Files

DO NOT BE LAZY - For EACH workspace file (SOUL.md, AGENTS.md, IDENTITY.md), launch a subprocess (or perform in main thread) that:

1. Loads the file
2. Checks for valid YAML frontmatter (if expected)
3. Verifies required sections are present (per checklist)
4. Returns structured findings:

```json
{
  "file": "[filename]",
  "exists": true/false,
  "frontmatter_valid": true/false/na,
  "required_sections_present": ["section1", "section2"],
  "required_sections_missing": ["section3"],
  "status": "PASS/FAIL/WARNING",
  "notes": "[any observations]"
}
```

### 3. Check Skill Files

DO NOT BE LAZY - For EACH of the 9 skill directories, launch a subprocess (or perform in main thread) that:

1. Checks that the skill directory exists
2. Loads the SKILL.md file
3. Verifies required elements: trigger examples, flow description, output specification
4. Returns structured findings per skill

### 4. Check Reference Data Files

For each expected reference data file (patterns library, config schema):

1. Verify the file exists
2. Check it has content (not empty)
3. Verify basic structure (headers, sections)
4. Record findings

### 5. Check Module Configuration

Verify module.yaml:
1. Contains required fields: code, name, header, subheader
2. Contains forge_artifacts variable definition
3. Valid YAML syntax

### 6. Compile Structural Findings

Append to the **Structural Validation** section of {outputFile}:

```markdown
### Workspace Files

| File | Exists | Frontmatter | Required Sections | Status |
|------|--------|-------------|-------------------|--------|
| SOUL.md | Y/N | Valid/Invalid/N/A | All present / Missing: [list] | PASS/FAIL |
| AGENTS.md | Y/N | Valid/Invalid/N/A | All present / Missing: [list] | PASS/FAIL |
| IDENTITY.md | Y/N | Valid/Invalid/N/A | All present / Missing: [list] | PASS/FAIL |

### Skill Files

| Skill | Directory | SKILL.md | Triggers | Flow | Output Spec | Status |
|-------|-----------|----------|----------|------|-------------|--------|
| design-system | Y/N | Y/N | Y/N | Y/N | Y/N | PASS/FAIL |
| [... all 9 skills ...] |

### Reference Data

| File | Exists | Has Content | Structure Valid | Status |
|------|--------|-------------|----------------|--------|
| Patterns library | Y/N | Y/N | Y/N | PASS/FAIL |
| Config schema | Y/N | Y/N | Y/N | PASS/FAIL |

### Module Configuration

| Check | Result | Status |
|-------|--------|--------|
| module.yaml exists | Y/N | PASS/FAIL |
| Required fields present | Y/N | PASS/FAIL |
| forge_artifacts defined | Y/N | PASS/FAIL |

### Structural Summary

- **Total checks:** [count]
- **Passed:** [count]
- **Failed:** [count]
- **Warnings:** [count]
```

Update {outputFile} frontmatter:
```yaml
stepsCompleted: ['step-01-init', 'step-02-structural']
lastStep: 'step-02-structural'
```

### 7. Present MENU OPTIONS

Display: "**Structural validation complete. Proceeding to coherence checks...**"

#### Menu Handling Logic:

- After structural findings are saved to {outputFile} and frontmatter updated, immediately load, read entire file, then execute {nextStepFile}

#### EXECUTION RULES:

- This is a validation sequence step with auto-proceed
- Proceed directly to next step after findings are saved

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN all structural checks are complete and findings are saved to {outputFile} will you then load and read fully {nextStepFile} to execute coherence validation.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All workspace files checked for structure
- All 9 skill files checked for required elements
- Reference data files verified
- Module configuration validated
- All findings recorded in {outputFile} with pass/fail status
- Summary counts accurate

### ❌ SYSTEM FAILURE:

- Skipping any file or check
- Not recording findings in the report
- Checking cross-references (wrong step)
- Not using structured findings format
- Being lazy — not checking every file

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
