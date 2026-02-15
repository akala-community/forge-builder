---
name: 'step-05-coherence-check'
description: 'Verify workspace consistency after edits and offer iteration'

nextStepFile: './step-06-completion.md'
loopBackStep: './step-02-identify-changes.md'
fixStep: './step-04-apply-changes.md'
outputFile: '{ocf_output_folder}/change-reports/change-report-{date}.md'
coherenceRulesData: '../data/coherence-rules.csv'
artifactTypesData: '../data/artifact-types.csv'
---

# Step 5: Coherence Check

## STEP GOAL:

To verify the workspace's internal consistency after all edits have been applied, checking every coherence rule and offering the user options to fix issues or make additional edits.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a quality assurance specialist verifying workspace integrity
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ Channel Cog (Gear Wright) for technical verification rigor
- ✅ Be thorough but not alarmist -- distinguish critical from advisory findings

### Step-Specific Rules:

- 🎯 Focus on verification -- check EVERY coherence rule
- 🚫 FORBIDDEN to modify files in this step -- only verify
- 💬 Present findings clearly with severity levels
- ⚙️ Use subprocess optimization (Pattern 4) for parallel coherence checks if available. TOOL/SUBPROCESS FALLBACK: If subprocess unavailable, perform checks sequentially in main thread

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append coherence results to {outputFile}
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to skip any coherence rule

## CONTEXT BOUNDARIES:

- All modifications have been applied (from step 4)
- The modification plan and applied changes are documented in the change report
- Focus: Post-edit verification of the ENTIRE workspace
- Limits: Verification only -- user decides what to fix

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Coherence Framework

Load `{coherenceRulesData}` for the full set of coherence rules.
Load `{artifactTypesData}` for artifact relationships.
Load `{outputFile}` to review what was modified.

"**Running coherence checks across the workspace...**

I'll verify {rule_count} coherence rules across all workspace artifacts."

### 2. Execute Coherence Checks

**For EACH coherence rule in {coherenceRulesData}:**

Read both the source and target artifacts referenced by the rule.

Check the specific condition described in the rule:

- **alignment:** Do the artifacts align in their intent and content?
- **reference:** Do cross-references resolve to existing files/sections?
- **coverage:** Are all required elements present?
- **internal:** Is the artifact internally consistent?

Record result:
- **PASS:** Rule satisfied
- **WARN:** Minor issue, not critical
- **FAIL:** Rule violated, needs attention

### 3. Present Coherence Results

"**Coherence Check Results:**

| Rule | Source | Target | Check | Result | Details |
|------|--------|--------|-------|--------|---------|
| CR001 | SOUL.md | AGENTS.md | alignment | {PASS/WARN/FAIL} | {details} |
| CR002 | AGENTS.md | skills/ | reference | {PASS/WARN/FAIL} | {details} |
| ... | ... | ... | ... | ... | ... |

---

**Summary:**
- **PASS:** {count} rules
- **WARN:** {count} rules
- **FAIL:** {count} rules

**Overall Status:** {CLEAN / WARNINGS / ISSUES FOUND}"

### 4. Detail Any Failures

If any rules FAILED:

"**Issues Found:**

**{rule_id}: {description}**
- **Source:** {source artifact} -- {what's there}
- **Target:** {target artifact} -- {what's expected}
- **Severity:** {critical/important}
- **Suggested Fix:** {how to resolve}

{Repeat for each failure}"

### 5. Detail Any Warnings

If any rules had WARNINGS:

"**Warnings:**

**{rule_id}: {description}**
- **Details:** {what's slightly off}
- **Recommendation:** {what could be improved}

{Repeat for each warning}"

### 6. Append to Change Report

Append to `{outputFile}`:

```markdown
## Coherence Check Results

**Check Date:** {current date}
**Rules Checked:** {total}
**Pass:** {count} | **Warn:** {count} | **Fail:** {count}
**Overall Status:** {status}

### Full Results

{Complete results table}

### Issues Found

{Detailed failures if any}

### Warnings

{Detailed warnings if any}

### Recommendations

{Any recommendations for further changes}
```

Update frontmatter:
- Add 'step-05-coherence-check' to stepsCompleted
- Set lastStep to 'step-05-coherence-check'

### 7. Present Menu Options

**IF no failures (CLEAN or WARNINGS only):**

Display: "**Coherence check passed. Select an Option:** [C] Complete -- finalize the change report [E] Edit More -- make additional changes"

**IF failures found:**

Display: "**Coherence issues found. Select an Option:** [F] Fix Issues -- apply corrections to resolve failures [E] Edit More -- make additional changes (including fixes) [C] Complete Anyway -- accept current state with known issues"

#### Menu Handling Logic:

- IF C: Save coherence results to {outputFile}, update frontmatter, then load, read entire file, then execute {nextStepFile}
- IF E: Save coherence results to {outputFile}, then load, read entire file, then execute {loopBackStep} (loop back to step 2 for new changes)
- IF F: Save coherence results to {outputFile}, then load, read entire file, then execute {fixStep} (loop back to step 4 to apply fixes)
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#7-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed when user makes a selection
- User can chat or ask questions -- always respond and then redisplay menu

## CRITICAL STEP COMPLETION NOTE

The user may loop back to step 2 (Edit More) or step 4 (Fix Issues) multiple times. Only when they select C (Complete) will you load {nextStepFile} for the completion step.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Every coherence rule checked
- Results clearly presented with severity levels
- Failures detailed with suggested fixes
- User given clear options (fix, edit more, or complete)
- Results saved to change report

### ❌ SYSTEM FAILURE:

- Skipping any coherence rule
- Not checking artifacts that were modified
- Not presenting failures clearly
- Modifying files during verification
- Proceeding without user decision on failures

**Master Rule:** Check EVERY rule. Present EVERY finding. Let the USER decide what to do about issues.
