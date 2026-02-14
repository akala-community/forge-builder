---
name: 'step-05-report'
description: 'Compile overall status, present installation report, offer next actions'

reportOutput: '{reportOutput}'
---

# Step 5: Installation Report

## STEP GOAL:

To compile the overall installation status from all steps, generate a summary with actionable recommendations, present the report to the user, and offer next actions.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- ⚙️ If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are the **Installation Specialist** — reporting results
- ✅ Clear, actionable feedback
- ✅ Objective summary — facts, not opinions

### Step-Specific Rules:

- 🎯 Focus on compiling the report and presenting it clearly
- 💬 Provide actionable recommendations for any FAIL or WARN items
- 🚫 FORBIDDEN to re-run checks — just compile and summarize

## EXECUTION PROTOCOLS:

- 🎯 Review all check sections and compile totals
- 💾 Append summary section to {reportOutput}
- ⏸️ HALT at menu and wait for user input (this is the final step)

## CONTEXT BOUNDARIES:

- All checks from steps 01-04 are complete and recorded in the report
- Focus on summarization and actionable guidance
- Dependencies: steps 01, 02, 03, and 04 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Compile Overall Status

Review all check sections in {reportOutput} and count:
- Total [PASS] across all sections
- Total [FAIL] across all sections
- Total [WARN] across all sections

Determine overall status:
- **PASS:** Zero [FAIL] items (warnings acceptable)
- **WARNINGS:** Zero [FAIL] items but one or more [WARN] items
- **FAIL:** One or more [FAIL] items

### 2. Generate Recommendations

For each [FAIL] item, create a **Priority 1 (Critical)** recommendation:
- What failed
- What the fix is
- Why it matters

For each [WARN] item, create a **Priority 2 (Recommended)** recommendation:
- What triggered the warning
- What the fix is
- Why it's recommended

### 3. Append Summary to Report

Replace the "## Summary" section in {reportOutput} with:

```markdown
## Summary

**Overall Status:** {PASS/WARNINGS/FAIL}

### Totals

| Category | Pass | Fail | Warn |
|----------|------|------|------|
| Package Validation | {n} | {n} | {n} |
| Extraction | {n} | {n} | {n} |
| Configuration | {n} | {n} | {n} |
| Registration | {n} | {n} | {n} |
| Activation | {n} | {n} | {n} |
| **Total** | **{n}** | **{n}** | **{n}** |

### Recommendations

#### Priority 1 — Critical (must fix)

{List each FAIL item with fix guidance, or "None — all critical checks passed."}

#### Priority 2 — Recommended (should fix)

{List each WARN item with fix guidance, or "None — no warnings."}

---

**Installation completed:** {current_date}
**Package:** {package_path}
**Target Workspace:** {target_workspace}
```

Update the report frontmatter:
```yaml
installationStatus: {PASS/WARNINGS/FAIL}
```

### 4. Present Report to User

"**Installation complete!**

**Overall Status:** {PASS/WARNINGS/FAIL}

**Results:**
- {pass_count} checks passed
- {fail_count} checks failed
- {warn_count} warnings

{If FAIL:}
**Critical issues found that must be fixed:**
{List each FAIL item briefly}

{If WARN:}
**Warnings to consider:**
{List top 3 WARN items briefly}

{If PASS and no warnings:}
**Package installed successfully. Agent system is ready to use.**

**Report saved to:** `{reportOutput}`"

### 5. Present MENU OPTIONS

Display: "**What would you like to do?**

- **[R]ead report** — Show the full installation report
- **[V]alidate workspace** — Run the validate-workspace workflow on the installed workspace
- **[D]one** — Complete installation"

#### Menu Handling Logic:

- IF R: Display the full content of {reportOutput}, then redisplay menu
- IF V: Suggest running the validate-workspace workflow on the installed workspace path, then redisplay menu
- IF D: Complete the installation session
- IF Any other comments or queries: help user respond, then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- User can chat or ask questions — always respond and redisplay menu

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Overall status correctly determined from all checks
- Pass/fail/warn totals accurate
- Actionable recommendations generated for every FAIL and WARN
- Summary appended to report
- Report presented clearly to user
- Menu presented with next actions

### ❌ SYSTEM FAILURE:

- Miscounting pass/fail/warn totals
- Not generating recommendations for failures
- Not saving summary to report
- Not presenting report to user

**Master Rule:** The report must be accurate, actionable, and clear. Compile everything from the previous steps into a useful summary.
