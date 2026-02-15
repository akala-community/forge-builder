---
name: 'step-04-completeness'
description: 'Run completeness validation checks — ensure all required components are present'

nextStepFile: './step-05-report.md'
outputFile: '{forge_artifacts}/validation-report.md'
validationChecklist: '../data/forge-validation-checklist.md'
---

# Step 4: Completeness Validation

## STEP GOAL:

To verify The Forge module has all required components — all 9 skills, all 5 BMAD build workflows, all 7 agentic patterns documented, and each skill has its required bundled resources.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are a quality inspector running completeness checks
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ This is an autonomous validation step — check counts and presence

### Step-Specific Rules:

- 🎯 Focus only on completeness — are all required components present?
- 🚫 FORBIDDEN to re-check structure or coherence — that was steps 2 and 3
- 💬 Use subprocess optimization (Pattern 3) to load module-brief and extract expected lists if available
- ⚙️ If subprocess unavailable, perform analysis in main thread

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append all findings to the Completeness Validation section of {outputFile}
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to proceed without completing all completeness checks

## CONTEXT BOUNDARIES:

- Available: Artifact inventory, structural findings, coherence findings
- Focus: Counting and presence — is everything that should be there, there?
- Limits: Do not re-check format or cross-references
- Dependencies: Steps 1, 2, and 3 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Completeness Criteria

Load {validationChecklist} and extract the **Completeness Checks** section. This defines all required components with exact names and counts.

### 2. Check Skills Completeness (9 Required)

Verify all 9 skills are present:

**Core Skills (3):**
1. design-system
2. add-agent
3. recommend-pattern

**Feature Skills (3):**
4. setup-knowledge
5. setup-harness
6. harden-workspace

**Utility Skills (3):**
7. validate-workspace
8. export-package
9. import-package

For each skill, verify:
- Skill directory exists
- SKILL.md file present
- Any expected bundled resources present

Record: Present count / Expected count, list any missing.

### 3. Check BMAD Build Workflows (5 Required)

Verify all 5 BMAD build workflows exist:

1. build-forge-agent
2. build-forge-skill
3. update-reference-data
4. package-forge
5. validate-forge

For each workflow, verify:
- Workflow directory or file exists

Record: Present count / Expected count, list any missing.

### 4. Check Agentic Patterns (7 Required)

Verify all 7 agentic patterns are documented in the patterns library:

1. Prompt Chaining
2. Routing
3. Parallelization
4. Orchestrator-Workers
5. Evaluator-Optimizer
6. Autonomous Agent
7. Long-Running Harness

For each pattern, verify:
- Pattern entry exists in patterns library
- Has description
- Has OpenClaw implementation guide

Record: Documented count / Expected count, list any missing.

### 5. Check Bundled Resources Per Skill

For each of the 9 skills, check that referenced templates and data files are bundled with the skill.

Record: Any skills with missing bundled resources.

### 6. Check for Orphan Files

Scan the artifacts directory for files that exist but are not referenced by any skill, workspace file, or workflow.

Record: List of orphan files as warnings.

### 7. Compile Completeness Findings

Append to the **Completeness Validation** section of {outputFile}:

```markdown
### Skills Completeness

| Category | Skill | Present | Status |
|----------|-------|---------|--------|
| Core | design-system | Y/N | PASS/FAIL |
| Core | add-agent | Y/N | PASS/FAIL |
| Core | recommend-pattern | Y/N | PASS/FAIL |
| Feature | setup-knowledge | Y/N | PASS/FAIL |
| Feature | setup-harness | Y/N | PASS/FAIL |
| Feature | harden-workspace | Y/N | PASS/FAIL |
| Utility | validate-workspace | Y/N | PASS/FAIL |
| Utility | export-package | Y/N | PASS/FAIL |
| Utility | import-package | Y/N | PASS/FAIL |

**Skills: [present]/9**

### BMAD Build Workflows

| Workflow | Present | Status |
|----------|---------|--------|
| build-forge-agent | Y/N | PASS/FAIL |
| build-forge-skill | Y/N | PASS/FAIL |
| update-reference-data | Y/N | PASS/FAIL |
| package-forge | Y/N | PASS/FAIL |
| validate-forge | Y/N | PASS/FAIL |

**Workflows: [present]/5**

### Agentic Patterns

| Pattern | Documented | Implementation Guide | Status |
|---------|------------|---------------------|--------|
| Prompt Chaining | Y/N | Y/N | PASS/FAIL |
| Routing | Y/N | Y/N | PASS/FAIL |
| Parallelization | Y/N | Y/N | PASS/FAIL |
| Orchestrator-Workers | Y/N | Y/N | PASS/FAIL |
| Evaluator-Optimizer | Y/N | Y/N | PASS/FAIL |
| Autonomous Agent | Y/N | Y/N | PASS/FAIL |
| Long-Running Harness | Y/N | Y/N | PASS/FAIL |

**Patterns: [documented]/7**

### Bundled Resources

| Skill | Resources Complete | Missing |
|-------|--------------------|---------|
| [skill] | Y/N | [list] |

### Orphan Files

| File | Path | Status |
|------|------|--------|
| [file] | [path] | WARNING - not referenced |

### Completeness Summary

- **Total checks:** [count]
- **Passed:** [count]
- **Failed:** [count]
- **Warnings:** [count]
```

Update {outputFile} frontmatter:
```yaml
stepsCompleted: ['step-01-init', 'step-02-structural', 'step-03-coherence', 'step-04-completeness']
lastStep: 'step-04-completeness'
```

### 8. Present MENU OPTIONS

Display: "**Completeness validation complete. Proceeding to final report...**"

#### Menu Handling Logic:

- After completeness findings are saved to {outputFile} and frontmatter updated, immediately load, read entire file, then execute {nextStepFile}

#### EXECUTION RULES:

- This is a validation sequence step with auto-proceed
- Proceed directly to next step after findings are saved

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN all completeness checks are complete and findings are saved to {outputFile} will you then load and read fully {nextStepFile} to compile the final report.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All 9 skills checked for presence
- All 5 BMAD workflows checked for presence
- All 7 agentic patterns checked for documentation
- Bundled resources per skill verified
- Orphan files identified
- Summary counts accurate

### ❌ SYSTEM FAILURE:

- Not checking all 9 skills by name
- Not checking all 5 workflows by name
- Not checking all 7 patterns by name
- Skipping orphan file check
- Being lazy — checking counts without verifying specific names

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
