---
name: 'step-05-report'
description: 'Calculate overall status, compile totals, generate recommendations, present final validation report, offer next actions'
---

# Step 5: Report

## STEP GOAL:

To calculate the overall validation status, compile pass/warning/error totals across all check categories, generate actionable recommendations from the findings, present the completed validation report, and offer the user a menu of next actions.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- CRITICAL: Read the complete step file before taking any action
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are a precision configuration validator (Cog / Gear Wright)
- Systematic, thorough, objective -- reports facts, not opinions
- You bring expertise in summarizing validation results and providing actionable guidance

### Step-Specific Rules:

- Focus ONLY on report compilation, status calculation, and next-action guidance
- FORBIDDEN to run any additional validation checks
- FORBIDDEN to modify any workspace files -- this is a read-only workflow
- Present clear, actionable results
- This is the FINAL step -- no next step file
- If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- Calculate overall status from all check results
- Compile totals per category and overall
- Generate recommendations from warnings and errors
- Complete the validation report
- Present the report to the user
- Offer a next-actions menu
- This is the FINAL step

## CONTEXT BOUNDARIES:

- Workspace path from step 01
- Workspace inventory from step 01
- Structural check results from step 02 (if it ran)
- Coherence check results from step 03 (if it ran)
- Hardening check results from step 04 (if it ran)
- Validation report with all check sections populated
- Dependencies: all previous steps that were selected must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Calculate Overall Status

Apply the status calculation rules:

| Condition | Overall Status |
|-----------|---------------|
| Zero ERRORs and zero WARNINGs | **PASS** |
| Zero ERRORs but one or more WARNINGs | **WARNINGS** |
| One or more ERRORs (regardless of WARNINGs) | **FAIL** |

Only count results from check categories that were actually run (based on user selection in step 01). SKIPPED checks do not count toward any category.

### 2. Compile Totals

Count the results across all categories that ran:

**Per category:**
- Structural: {pass} PASS / {warn} WARNING / {error} ERROR
- Coherence: {pass} PASS / {warn} WARNING / {error} ERROR
- Hardening: {pass} PASS / {warn} WARNING / {error} ERROR / {info} INFO

**Overall totals:**
- Total PASS: sum across all categories
- Total WARNING: sum across all categories
- Total ERROR: sum across all categories
- Total INFO: sum across all categories (hardening only)
- Total SKIPPED: sum across all categories

### 3. Generate Recommendations

Based on the findings, generate a prioritized list of recommendations:

**For each ERROR found:**
- Generate a "CRITICAL" recommendation explaining what is wrong and how to fix it
- Example: "CRITICAL: AGENTS.md is missing. Create AGENTS.md with agent directives, startup sequence, and skill bindings."

**For each WARNING found:**
- Generate a "RECOMMENDED" recommendation explaining what could be improved
- Example: "RECOMMENDED: SOUL.md does not define operational boundaries. Add a Boundaries section to SOUL.md specifying what the agent will and will not do."

**For INFO items:**
- Generate "CONSIDER" recommendations where improvement is possible
- Example: "CONSIDER: Compaction mode is 'default'. Switch to 'safeguard' mode in openclaw.json for better memory preservation."

Order recommendations: CRITICAL first, then RECOMMENDED, then CONSIDER.

### 4. Complete the Validation Report

Fill in the Summary section of the validation report:

- **Overall Status:** the calculated status
- **Category totals table:** filled with per-category and overall counts
- **Recommendations:** the generated recommendation list

Update the header **Overall Status** field from PENDING to the calculated status.

### 5. Present the Report

"**Workspace Validation Report**

---

**Workspace:** `{workspace_path}`
**Date:** {validation_date}
**Checks Run:** {checks_that_ran}
**Overall Status:** {overall_status}

---

### Results Summary

| Category | PASS | WARNING | ERROR | INFO |
|----------|------|---------|-------|------|
| Structural | {s_pass} | {s_warn} | {s_error} | - |
| Coherence | {c_pass} | {c_warn} | {c_error} | - |
| Hardening | {h_pass} | {h_warn} | {h_error} | {h_info} |
| **Total** | **{total_pass}** | **{total_warn}** | **{total_error}** | **{total_info}** |

---

### Recommendations

{numbered list of recommendations, ordered by priority}

---

**Select:** [R] Read full detailed report | [F] Fix issues (show fix guidance) | [D] Done"

### 6. Menu Handling

#### Menu Handling Logic:

- **IF R:** Present the complete validation report with all individual check results (the full Structural Checks, Coherence Checks, and Hardening Checks tables from previous steps). After presenting, redisplay the menu.

- **IF F:** For each ERROR and WARNING, present specific fix instructions:
  - For missing files: Provide the file name and a brief description of what it should contain, suggest using a creation workflow if applicable
  - For consistency issues: Explain what needs to align and in which files
  - For missing configuration: Show the openclaw.json field path and recommended values
  - For missing directives: Describe what section or content to add and to which file
  - After presenting fix guidance, redisplay the menu.

- **IF D:**
  "**Validation complete.** The report has been compiled. You can re-run this workflow at any time to check for improvements."
  End the workflow.

- **IF any other input:** Help the user with their question or concern, then redisplay the menu.

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting the menu
- ONLY end the workflow when user selects 'D'
- For 'R' and 'F', always return to the menu after presenting information

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Overall status correctly calculated from all check results
- Totals accurately compiled per category and overall
- Recommendations generated for every ERROR, WARNING, and relevant INFO
- Recommendations properly prioritized (CRITICAL > RECOMMENDED > CONSIDER)
- Complete validation report presented with summary table
- Menu presented and handled correctly
- No files modified during this step

### FAILURE:

- Miscounting pass/warning/error totals
- Not generating recommendations for all issues found
- Not presenting a clear summary table
- Running additional validation checks in this step
- Not offering the next-actions menu
- Modifying any workspace files
- Not waiting for user input at the menu

**Master Rule:** This is the final step. Calculate status, compile totals, generate recommendations, present the report, offer next actions. DO NOT run any checks or modify any files.
