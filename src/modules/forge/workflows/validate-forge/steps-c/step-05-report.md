---
name: 'step-05-report'
description: 'Compile final validation report with overall verdict'

outputFile: '{forge_artifacts}/validation-report.md'
---

# Step 5: Final Report & Verdict

## STEP GOAL:

To compile all validation findings into an overall verdict, update the executive summary, and present the final validation report to the user.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are a quality inspector delivering the final assessment
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ Present findings objectively and clearly

### Step-Specific Rules:

- 🎯 Focus only on compiling results and determining verdict
- 🚫 FORBIDDEN to run new validation checks — all checks are done
- 💬 Present results clearly with actionable recommendations

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Update {outputFile} with executive summary and overall verdict
- 📖 Mark report as complete in frontmatter
- 🚫 This is the final step — no next step to load

## CONTEXT BOUNDARIES:

- Available: Complete validation report with findings from steps 1-4
- Focus: Aggregation and verdict only
- Limits: Do not re-run any checks
- Dependencies: All previous steps must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Complete Report

Load {outputFile} and review all findings from:
- Step 1: Artifact Inventory
- Step 2: Structural Validation
- Step 3: Coherence Validation
- Step 4: Completeness Validation

### 2. Aggregate Counts

Calculate totals across all validation categories:

- **Total checks performed:** [sum of all checks]
- **Total passed:** [sum of all passes]
- **Total failed:** [sum of all failures]
- **Total warnings:** [sum of all warnings]

### 3. Determine Overall Verdict

Apply verdict criteria:

| Verdict | Condition |
|---------|-----------|
| **PASS** | 0 failures AND 0 warnings |
| **PASS WITH WARNINGS** | 0 failures AND >0 warnings |
| **FAIL** | >0 failures |

### 4. Compile Executive Summary

Update the **Executive Summary** section of {outputFile}:

```markdown
## Executive Summary

**Overall Verdict: [PASS / PASS WITH WARNINGS / FAIL]**

| Category | Checks | Passed | Failed | Warnings |
|----------|--------|--------|--------|----------|
| Structural | [n] | [n] | [n] | [n] |
| Coherence | [n] | [n] | [n] | [n] |
| Completeness | [n] | [n] | [n] | [n] |
| **Total** | **[n]** | **[n]** | **[n]** | **[n]** |

[If FAIL]:
### Critical Issues Requiring Resolution

1. [Most important failure with brief description]
2. [Second failure]
...

[If PASS WITH WARNINGS]:
### Warnings to Review

1. [Warning with brief description]
2. [Second warning]
...

[If PASS]:
All checks passed. The Forge module is internally consistent and ready for packaging.
```

### 5. Update Overall Verdict Section

Update the **Overall Verdict** section at the end of {outputFile}:

```markdown
## Overall Verdict

**[PASS / PASS WITH WARNINGS / FAIL]**

**Validated:** [date]
**Total checks:** [count]
**Pass rate:** [percentage]%

[If FAIL]:
**Action required:** Resolve the [count] critical issues listed in the Executive Summary before packaging or deployment. Re-run validation after fixes.

[If PASS WITH WARNINGS]:
**Recommendation:** Review the [count] warnings listed in the Executive Summary. These do not block packaging but may indicate areas for improvement.

[If PASS]:
**Status:** The Forge module has passed all validation checks and is cleared for packaging and deployment.
```

### 6. Finalize Report

Update {outputFile} frontmatter:
```yaml
stepsCompleted: ['step-01-init', 'step-02-structural', 'step-03-coherence', 'step-04-completeness', 'step-05-report']
lastStep: 'step-05-report'
verdict: '[PASS / PASS WITH WARNINGS / FAIL]'
totalChecks: [count]
passed: [count]
failed: [count]
warnings: [count]
```

### 7. Present Final Report to User

"**Forge Module Validation Complete**

**Verdict: [PASS / PASS WITH WARNINGS / FAIL]**

**Results:**
- Total checks: [count]
- Passed: [count]
- Failed: [count]
- Warnings: [count]

**Full report saved to:** `{outputFile}`

[If FAIL]:
Please review the critical issues in the report and re-run validation after fixes.

[If PASS WITH WARNINGS]:
Module is ready for packaging. Review warnings at your convenience.

[If PASS]:
Module is internally consistent and ready for packaging."

## CRITICAL STEP COMPLETION NOTE

This is the FINAL step. No further steps to load. The workflow is complete when the report is saved and presented to the user.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All findings aggregated correctly
- Overall verdict determined by criteria (not subjective)
- Executive summary populated with clear results
- Critical issues listed for FAIL verdict
- Warnings listed for PASS WITH WARNINGS
- Report frontmatter updated with final counts and verdict
- Report presented clearly to user

### ❌ SYSTEM FAILURE:

- Incorrect aggregation of counts
- Subjective verdict (not based on criteria)
- Missing executive summary
- Not updating frontmatter with verdict
- Running new checks in this step

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
