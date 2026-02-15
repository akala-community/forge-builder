---
name: 'step-06-completion'
description: 'Present change report summary and offer validate-workspace chaining'

outputFile: '{ocf_output_folder}/change-reports/change-report-{date}.md'
---

# Step 6: Completion

## STEP GOAL:

Complete the edit-agent-system workflow with a summary of all changes made, the final coherence status, and guidance on next steps.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER modify the workspace at this stage
- 📖 CRITICAL: Read the complete step file before taking any action
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a workflow completion specialist
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ Present a clear, professional summary

### Step-Specific Rules:

- 🎯 Focus ONLY on summary and next steps
- 🚫 FORBIDDEN to modify the workspace or change report content
- 💬 Present completion clearly and positively

## EXECUTION PROTOCOLS:

- 🎯 Present completion summary
- 💾 Finalize change report
- 📖 Provide next steps guidance
- 🚫 No more modifications at this stage

## CONTEXT BOUNDARIES:

- All changes have been applied and verified
- Coherence check results are documented
- This is the final step

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly.

### 1. Load Change Report

Load `{outputFile}` completely to extract summary data.

### 2. Present Completion Summary

"**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

# Edit Agent System -- Complete!

**Workspace:** {workspacePath}
**Date:** {date}
**Editor:** {user_name}

---

## Changes Applied

**Total Changes Requested:** {count}
**Total Files Modified:** {count}
**Total Files Skipped:** {count}

### Modification Summary

| File | Change Type | Status |
|------|-------------|--------|
{summary table from step 4}

---

## Coherence Status

**Overall:** {CLEAN / WARNINGS / ISSUES ACCEPTED}
**Rules Checked:** {count}
**Pass:** {count} | **Warn:** {count} | **Fail:** {count}

{If any warnings or accepted issues, list them briefly}

---

## Change Report

**Full change report saved to:** {outputFile}

The report contains:
- Workspace inventory
- Change specifications
- Impact analysis
- Per-file modification details (before/after)
- Coherence check results

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**"

### 3. Finalize Change Report

Update `{outputFile}` frontmatter:

- Add 'step-06-completion' to stepsCompleted
- Set lastStep to 'step-06-completion'
- Set status to COMPLETE
- Set completionDate to {current date}

Append to `{outputFile}`:

```markdown
---

## Session Complete

**Completion Date:** {date}
**Status:** COMPLETE
**Overall Coherence:** {status}
```

### 4. Provide Next Steps Guidance

"**Next Steps:**

**Validate your workspace:**
- Run the **validate-workspace** workflow for a comprehensive consistency check
- Command: Activate Cog (Gear Wright) and use `[VW] Validate Workspace`

**Further edits:**
- Run this workflow again to make additional changes
- Each session creates a new change report for traceability

**Package for deployment:**
- Use **package-export** to bundle the updated workspace
- Command: Activate Cog and use `[PE] Package Export`

**Review the change report:**
- Full report at: {outputFile}
- Contains complete before/after documentation of all changes"

### 5. Final Message

"**Thank you for using Edit Agent System!**

Your workspace at **{workspacePath}** has been updated with {change_count} modifications.

**Change report:** {outputFile}"

## CRITICAL STEP COMPLETION NOTE

This is the final step. Present completion summary, finalize the change report, and provide next steps. No further modifications.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Completion summary presented clearly
- Change report finalized with COMPLETE status
- Next steps guidance provided (validate, package, further edits)
- Session ends positively

### ❌ SYSTEM FAILURE:

- Not providing clear summary
- Not finalizing change report status
- Missing next steps guidance

**Master Rule:** End on a positive note with clear summary and actionable next steps.
