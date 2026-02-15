---
name: 'step-06-validate'
description: 'Cross-check the new skill against existing skills for naming collisions, trigger conflicts, and pattern overlap'

nextStepFile: './step-07-complete.md'
outputFile: '{forge_artifacts}/add-skill-context.md'
skillOutputPath: '{project-root}/_bmad/forge/skills/{skillName}/SKILL.md'
existingSkillsFolder: '{project-root}/_bmad/forge/skills'
forgeBuilderSpecFile: '{project-root}/src/modules/forge/agents/forge-builder.spec.md'
forgeSpecFile: '{project-root}/src/modules/forge/agents/forge.spec.md'
---

# Step 6: Validate Consistency

## STEP GOAL:

Cross-check the new skill against all existing skills and agent specifications for naming collisions, trigger conflicts, pattern overlap, and structural completeness. Present a validation report and offer to fix any issues.

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

- 🎯 Run all validation checks against the new skill
- 💾 Append validation report to {outputFile}
- 📖 Update {outputFile} frontmatter stepsCompleted when validation is complete
- 🚫 FORBIDDEN to skip validation checks

## CONTEXT BOUNDARIES:

- Available: New SKILL.md, updated agent specs, existing skills, module artifacts
- Focus: Validate quality, consistency, and conflict-free integration
- Limits: Report findings — user decides on fixes
- Dependencies: steps 01-05 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Files for Validation

Load:
- `{skillOutputPath}` — the generated SKILL.md
- `{existingSkillsFolder}/` — all existing skill directories and SKILL.md files
- `{forgeBuilderSpecFile}` — updated Forge Builder spec
- `{forgeSpecFile}` — updated Forge spec (if modified)

"**Running validation checks for: {skillName}**"

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

**Check 2: Naming Collision**
- [ ] Skill name is unique (not used by any existing skill)
- [ ] Skill name follows kebab-case convention
- [ ] Skill name doesn't conflict with any BMAD Core workflow names

**Check 3: Trigger Conflict**
- [ ] Trigger code (2-letter) is unique in Forge Builder command table
- [ ] Trigger code is unique in The Forge command table (if added)
- [ ] Trigger phrases don't overlap significantly with existing skill triggers
- [ ] Both primary and contextual triggers defined

**Check 4: Registration Integrity**
- [ ] Forge Builder spec has the new command table entry
- [ ] Command table entry matches SKILL.md metadata (name, description)
- [ ] If user-facing: The Forge spec also has the command table entry

**Check 5: Documentation Completeness**
- [ ] module-help.csv has an entry for the new skill
- [ ] docs/workflows.md has a section for the new skill
- [ ] Workflow count in docs/workflows.md is accurate

**Check 6: Connected Skills Consistency**
- [ ] Skills listed in "Leads to" exist or are planned
- [ ] Skills listed in "Triggered by" exist or are planned
- [ ] No circular dependencies

### 3. Present Validation Report

"**Validation Report: {skillName}**

---

**Check 1: Structural Completeness** — {PASS/FAIL}
{Details of any missing sections}

**Check 2: Naming Collision** — {PASS/FAIL}
{Details of any naming issues}

**Check 3: Trigger Conflict** — {PASS/FAIL}
{Details of any trigger conflicts}

**Check 4: Registration Integrity** — {PASS/FAIL}
{Details of any registration issues}

**Check 5: Documentation Completeness** — {PASS/FAIL}
{Details of any documentation gaps}

**Check 6: Connected Skills Consistency** — {PASS/FAIL}
{Details of any dependency issues}

---

**Overall: {X}/6 checks passed**

{If all pass: 'All validation checks passed. The skill is ready for the build pipeline.'}
{If some fail: 'Some checks need attention. Would you like me to fix the issues listed above?'}"

### 4. Handle Fixes (If Requested)

If user requests fixes:
- Apply requested changes to affected files
- Re-run affected validation checks
- Present updated results
- Iterate until user is satisfied or accepts as-is

### 5. Update Output File

Append to `{outputFile}`:

```markdown
---

## Validation Report

**Date:** {current date}
**Skill:** {skillName}
**Result:** {X}/6 checks passed
**Status:** {VALIDATED / VALIDATED_WITH_NOTES}

### Check Results
{Summary of each check result}

### Issues Found
{List of any issues, or 'None'}

### Fixes Applied
{List of any fixes, or 'None requested'}
```

Update frontmatter:
```yaml
stepsCompleted: ['step-01-define-concept', 'step-02-load-context', 'step-03-generate-spec', 'step-04-register-skill', 'step-05-update-artifacts', 'step-06-validate']
```

### 6. Present MENU OPTIONS

Display: **Validation complete. Select an option:** [C] Continue to Completion

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

#### Menu Handling Logic:

- IF C: Update {outputFile} frontmatter with stepsCompleted, then load, read entire file, then execute {nextStepFile}
- IF Any other: help user respond (apply fixes if requested), then [Redisplay Menu Options](#6-present-menu-options)

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All 6 validation checks executed
- Clear validation report presented
- User had opportunity to request fixes
- Fixes applied if requested
- Validation report appended to output file
- stepsCompleted fully updated

### ❌ SYSTEM FAILURE:

- Skipping validation checks
- Auto-fixing without user approval
- Vague validation report (no specifics)
- Not checking for trigger conflicts
- Not verifying registration integrity

**Master Rule:** Every check must run. Report findings honestly. User decides on fixes. Skipping steps is FORBIDDEN.
