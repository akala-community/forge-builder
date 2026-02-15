---
name: 'step-05-validate'
description: 'Validate the generated SKILL.md and data files for completeness and consistency'

outputFile: '{forge_output_folder}/skill-build-context.md'
skillOutputPath: '{forge_skills_folder}/{selectedSkill}/SKILL.md'
skillDataPath: '{forge_skills_folder}/{selectedSkill}/data'
skillRegistryData: '../data/skill-registry.md'
---

# Step 5: Validate Skill

## STEP GOAL:

Validate the generated SKILL.md and bundled data files for completeness, consistency, and alignment with the module brief. Present a validation report and offer to build another skill.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Morgan, the Forge Builder — a module build engineer
- ✅ You bring expertise in quality assurance for skill definitions
- ✅ Be thorough and honest — flag issues, don't hide them
- ✅ User decides whether to fix issues or accept as-is

### Step-Specific Rules:

- 🎯 Focus ONLY on validation — do not modify files unless user requests fixes
- 🚫 FORBIDDEN to auto-fix issues without user approval
- 💬 Present clear, actionable validation findings
- 🎯 Use subprocess Pattern 4 for parallel validation checks if available
- ⚙️ If subprocess unavailable, run checks sequentially in main thread

## EXECUTION PROTOCOLS:

- 🎯 Run all validation checks against SKILL.md and data files
- 💾 Append validation report to {outputFile}
- 📖 Update {outputFile} frontmatter stepsCompleted when validation is complete
- 🚫 FORBIDDEN to skip validation checks

## CONTEXT BOUNDARIES:

- Available: Generated SKILL.md, data files, module brief context, skill registry
- Focus: Validate quality, completeness, and consistency
- Limits: Report findings — user decides on fixes
- Dependencies: step-03 and step-04 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Files for Validation

Load:
- `{skillOutputPath}` — the generated SKILL.md
- `{skillDataPath}/` — any generated data files (list directory)
- `{outputFile}` — context and generation history

"**Running validation checks for: {selectedSkill}**"

### 2. Run Validation Checks

Run these checks (in parallel via subprocess Pattern 4 if available, sequentially if not):

**Check 1: Structural Completeness**
- [ ] SKILL.md has frontmatter (name, description, category, version)
- [ ] Triggers section present with activation phrases
- [ ] Execution Flow section present with numbered steps
- [ ] Instructions section present with role, behavior, detailed instructions
- [ ] Data Dependencies section present
- [ ] Connected Skills section present
- [ ] Success Criteria section present

**Check 2: Trigger Consistency**
- [ ] Trigger examples match the skill's purpose
- [ ] Trigger examples align with module brief trigger examples
- [ ] Both primary and contextual triggers defined
- [ ] Triggers don't overlap significantly with other skills' triggers

**Check 3: Flow Completeness**
- [ ] Every flow step has input, output, and user interaction defined
- [ ] Flow steps follow a logical sequence
- [ ] Flow covers the complete journey from trigger to completion
- [ ] No orphan steps (steps with no predecessor or successor)

**Check 4: Instruction Coverage**
- [ ] Instructions cover all flow steps
- [ ] Instructions are actionable (an LLM can follow them)
- [ ] Error handling / edge cases addressed
- [ ] Collaboration points clearly marked

**Check 5: Data File References**
- [ ] Every data file referenced in SKILL.md exists in data/
- [ ] No orphan data files (files that exist but aren't referenced)
- [ ] Data files are complete and non-empty

**Check 6: Brief Alignment**
Load `{skillRegistryData}` and cross-check:
- [ ] Skill purpose matches registry description
- [ ] Flow aligns with registry flow summary
- [ ] Connected skills match registry connections
- [ ] Category is correct (core/feature/utility)

### 3. Present Validation Report

"**Validation Report: {selectedSkill}**

---

**Check 1: Structural Completeness** — {PASS/FAIL}
{Details of any missing sections}

**Check 2: Trigger Consistency** — {PASS/FAIL}
{Details of any trigger issues}

**Check 3: Flow Completeness** — {PASS/FAIL}
{Details of any flow gaps}

**Check 4: Instruction Coverage** — {PASS/FAIL}
{Details of any instruction gaps}

**Check 5: Data File References** — {PASS/FAIL}
{Details of any reference mismatches}

**Check 6: Brief Alignment** — {PASS/FAIL}
{Details of any alignment issues}

---

**Overall: {X}/6 checks passed**

{If all pass: "All validation checks passed. The skill is ready for use."}
{If some fail: "Some checks need attention. Would you like me to fix the issues listed above?"}
"

### 4. Handle Fixes (If Requested)

If user requests fixes:
- Apply requested changes to SKILL.md and/or data files
- Re-run affected validation checks
- Present updated results
- Iterate until user is satisfied or accepts as-is

### 5. Update Output File

Append to `{outputFile}`:

```markdown
---

## Validation Report

**Date:** {current date}
**Skill:** {selectedSkill}
**Result:** {X}/6 checks passed
**Status:** {VALIDATED / VALIDATED_WITH_NOTES}

### Check Results
{Summary of each check result}

### Issues Found
{List of any issues, or "None"}

### Fixes Applied
{List of any fixes, or "None requested"}
```

Update frontmatter:
```yaml
stepsCompleted: ['step-01-select-skill', 'step-02-load-context', 'step-03-generate-skill', 'step-04-bundle-resources', 'step-05-validate']
status: COMPLETE
```

### 6. Present Completion Menu

"**Skill build complete for: {selectedSkill}**

**Files created:**
- `{skillOutputPath}`
- {list any data files}

**Validation:** {X}/6 passed

---

**Would you like to build another skill?**"

Display: **Select an option:** [B] Build Another Skill [D] Done

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- Route based on user selection

#### Menu Handling Logic:

- IF B: Reset workflow — load, read entire file, then execute `./step-01-select-skill.md` to start a new skill build
- IF D: "**All done. The following skills have been built in this session:** {list}. The Forge is one step closer to completion."
- IF Any other: help user respond, then [Redisplay Menu Options](#6-present-completion-menu)

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All 6 validation checks executed
- Clear validation report presented
- User had opportunity to request fixes
- Fixes applied if requested
- Validation report appended to output file
- stepsCompleted fully updated
- User offered to build another skill

### ❌ SYSTEM FAILURE:

- Skipping validation checks
- Auto-fixing without user approval
- Vague validation report (no specifics)
- Not offering to build another skill
- Not updating output file status

**Master Rule:** Every check must run. Report findings honestly. User decides on fixes. Skipping steps is FORBIDDEN.
