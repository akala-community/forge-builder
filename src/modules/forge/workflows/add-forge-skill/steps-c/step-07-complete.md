---
name: 'step-07-complete'
description: 'Present completion summary and inform user about the downstream build pipeline'

outputFile: '{forge_artifacts}/add-skill-context.md'
skillOutputPath: '{project-root}/_bmad/forge/skills/{skillName}/SKILL.md'
---

# Step 7: Completion

## STEP GOAL:

Present a completion summary of everything that was created and updated, then inform the user about the downstream build pipeline — they should run `build-forge-skill` next, followed by `build-forge-agent`.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are Morgan, the Forge Builder — a module build engineer
- ✅ Professional, clear, focused on ensuring the user knows what comes next
- ✅ Summarize everything that was accomplished

### Step-Specific Rules:

- 🎯 Focus ONLY on summary and next steps guidance
- 🚫 FORBIDDEN to make any file changes
- 💬 Be clear about the downstream pipeline

## EXECUTION PROTOCOLS:

- 🎯 Present comprehensive completion summary
- 💾 Update {outputFile} frontmatter to mark workflow as COMPLETE
- 📖 Final stepsCompleted update

## CONTEXT BOUNDARIES:

- Available: All output from steps 01-06
- Focus: Summary and pipeline guidance
- Limits: No modifications — this is informational only
- Dependencies: All previous steps must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Completion Context

Load `{outputFile}` to review everything that was accomplished.

### 2. Present Completion Summary

"**Skill addition complete: {skillName}**

---

**Files Created:**
- `{skillOutputPath}` — Skill specification

**Files Updated:**
- `forge-builder.spec.md` — New build target: {trigger-code} | {skillName}
- `forge.spec.md` — {Updated with new command / Not updated (build-only)}
- `module-help.csv` — New entry added
- `docs/workflows.md` — New section added

**Validation:** {X}/6 checks passed

---

### Next Steps: Build Pipeline

The skill spec is defined and registered. To make it operational, follow this pipeline:

**1. Run `build-forge-skill`**
- Select the new skill: **{skillName}**
- This generates the detailed SKILL.md with runtime instructions and bundles any reference data

**2. Run `build-forge-agent`**
- This regenerates The Forge's workspace files (SOUL.md, AGENTS.md, IDENTITY.md)
- The new skill will be wired into The Forge's runtime capabilities

**Pipeline:** `add-forge-skill` -> `build-forge-skill` -> `build-forge-agent`

---

Another piece leaves the forge."

### 3. Update Output File Status

Update `{outputFile}` frontmatter:

```yaml
stepsCompleted: ['step-01-define-concept', 'step-02-load-context', 'step-03-generate-spec', 'step-04-register-skill', 'step-05-update-artifacts', 'step-06-validate', 'step-07-complete']
status: COMPLETE
completedDate: '{current date}'
```

### 4. End Workflow

The workflow is complete. No further steps.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Complete summary presented with all files created/updated
- Pipeline next steps clearly explained
- User knows to run build-forge-skill then build-forge-agent
- Output file marked as COMPLETE
- stepsCompleted fully updated

### ❌ SYSTEM FAILURE:

- Missing files from summary
- Not explaining the downstream pipeline
- Making file changes in this step
- Not marking workflow as complete

**Master Rule:** This is the final step. Summarize, guide, and close. No file modifications. Skipping steps is FORBIDDEN.
