---
name: 'step-03-coherence'
description: 'Run coherence validation checks — cross-reference artifacts for internal consistency'

nextStepFile: './step-04-completeness.md'
outputFile: '{forge_artifacts}/validation-report.md'
validationChecklist: '../data/forge-validation-checklist.md'
---

# Step 3: Coherence Validation

## STEP GOAL:

To cross-reference Forge artifacts for internal consistency — verify that skills reference valid patterns, config fields exist in schema, agent names are consistent across files, and workflow connections match actual files.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are a quality inspector running coherence checks
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ This is an autonomous validation step — run cross-reference checks and record findings

### Step-Specific Rules:

- 🎯 Focus only on cross-referencing between artifacts — does A match B?
- 🚫 FORBIDDEN to re-check structural issues — that was step 2
- 🚫 FORBIDDEN to check completeness counts — that's step 4
- 💬 Use subprocess optimization (Pattern 2) for per-skill cross-reference analysis if available
- ⚙️ If subprocess unavailable, perform analysis in main thread

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append all findings to the Coherence Validation section of {outputFile}
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to proceed without completing all coherence checks

## CONTEXT BOUNDARIES:

- Available: Artifact inventory from Step 1, structural findings from Step 2
- Focus: Cross-references between artifacts — consistency checks
- Limits: Do not re-check file existence or format (already done)
- Dependencies: Steps 1 and 2 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Cross-Reference Rules

Load {validationChecklist} and extract the **Coherence Checks** section. This defines all cross-reference rules (CR-01 through CR-07).

### 2. CR-01: Module Brief vs Skill Files

Load the module-brief-forge.md and extract the list of 9 skills. For each skill listed in the brief, verify a corresponding skill file exists in the artifacts.

Record: Which skills from brief have files, which don't.

### 3. CR-02: Skill Pattern References vs Patterns Library

DO NOT BE LAZY - For EACH skill file, launch a subprocess (or perform in main thread) that:

1. Loads the skill file
2. Extracts any references to agentic patterns (Prompt Chaining, Routing, etc.)
3. Cross-references against the patterns library
4. Returns findings: which references are valid, which are orphaned

### 4. CR-03: Skill Config References vs Config Schema

DO NOT BE LAZY - For EACH skill file, check if it references OpenClaw configuration fields. Verify each referenced field exists in the config schema reference.

### 5. CR-04: Agent Name Consistency

Load IDENTITY.md, SOUL.md, and AGENTS.md. Extract the agent name from each. Verify the name is consistent across all three files.

### 6. CR-05: Workflow Connections vs Actual Files

Load the module brief's workflow connections section. For each workflow referenced, verify the corresponding workflow file exists.

### 7. CR-06: Skill Trigger Overlap

Extract trigger examples from all 9 skill files. Check for potential overlaps — triggers that could match multiple skills.

Record: Any overlapping triggers as warnings.

### 8. CR-07: Personality Consistency

Compare personality traits and communication style between SOUL.md and IDENTITY.md. Flag any contradictions.

### 9. Compile Coherence Findings

Append to the **Coherence Validation** section of {outputFile}:

```markdown
### Cross-Reference Results

| Rule | Description | Result | Status |
|------|-------------|--------|--------|
| CR-01 | Brief skills vs actual files | [details] | PASS/FAIL |
| CR-02 | Skill pattern refs vs library | [details] | PASS/FAIL |
| CR-03 | Skill config refs vs schema | [details] | PASS/FAIL/WARNING |
| CR-04 | Agent name consistency | [details] | PASS/FAIL |
| CR-05 | Workflow connections vs files | [details] | PASS/FAIL |
| CR-06 | Skill trigger overlap | [details] | PASS/WARNING |
| CR-07 | Personality consistency | [details] | PASS/WARNING |

### Detailed Findings

[For each FAIL or WARNING, provide specific details:]

**CR-[XX]: [Rule Name]**
- Issue: [what's wrong]
- Source: [file where reference exists]
- Target: [file where target should exist]
- Recommendation: [how to fix]

### Coherence Summary

- **Total checks:** [count]
- **Passed:** [count]
- **Failed:** [count]
- **Warnings:** [count]
```

Update {outputFile} frontmatter:
```yaml
stepsCompleted: ['step-01-init', 'step-02-structural', 'step-03-coherence']
lastStep: 'step-03-coherence'
```

### 10. Present MENU OPTIONS

Display: "**Coherence validation complete. Proceeding to completeness checks...**"

#### Menu Handling Logic:

- After coherence findings are saved to {outputFile} and frontmatter updated, immediately load, read entire file, then execute {nextStepFile}

#### EXECUTION RULES:

- This is a validation sequence step with auto-proceed
- Proceed directly to next step after findings are saved

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN all coherence checks are complete and findings are saved to {outputFile} will you then load and read fully {nextStepFile} to execute completeness validation.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All 7 cross-reference rules checked
- Each check produces a clear PASS/FAIL/WARNING result
- Detailed findings recorded for each failure or warning
- Recommendations provided for each issue
- Summary counts accurate

### ❌ SYSTEM FAILURE:

- Skipping any cross-reference rule
- Not loading actual file contents to check references
- Not recording detailed findings for failures
- Being lazy — surface-level checks instead of deep cross-referencing
- Checking structural issues (wrong step)

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
