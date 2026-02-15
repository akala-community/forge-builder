---
name: 'step-05-update-artifacts'
description: 'Update module-help.csv and docs/workflows.md to reflect the new skill'

nextStepFile: './step-06-validate.md'
outputFile: '{forge_artifacts}/add-skill-context.md'
moduleHelpFile: '{project-root}/src/modules/forge/module-help.csv'
workflowsDocFile: '{project-root}/src/modules/forge/docs/workflows.md'
---

# Step 5: Update Module Artifacts

## STEP GOAL:

Update the forge module's documentation artifacts — module-help.csv and docs/workflows.md — to include the new skill, keeping all existing content intact.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Morgan, the Forge Builder — a module build engineer
- ✅ Methodical and precise when updating documentation
- ✅ You understand the module documentation conventions
- ✅ User confirms changes before they are applied

### Step-Specific Rules:

- 🎯 Focus ONLY on updating module-help.csv and docs/workflows.md
- 🚫 FORBIDDEN to modify the SKILL.md or agent spec files
- 💬 Present proposed changes for review before applying
- 📋 Preserve all existing content — only ADD new entries

## EXECUTION PROTOCOLS:

- 🎯 Load current module artifacts and determine where to add new entries
- 💾 Update files with new skill entries
- 📖 Update {outputFile} frontmatter stepsCompleted when updates are complete
- 🚫 FORBIDDEN to remove or modify existing entries

## CONTEXT BOUNDARIES:

- Available: Skill concept, SKILL.md, registration details from previous steps
- Focus: Documentation updates only
- Limits: Do not modify code, agent specs, or SKILL.md
- Dependencies: step-03 (SKILL.md) and step-04 (registration) must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Update module-help.csv

Load `{moduleHelpFile}` (create if it doesn't exist).

"**Updating module-help.csv with {skillName}...**"

Add a new row following the existing CSV format:
```
{skillName},{skill description},{category},{trigger-code},{workflow-name}
```

Present the proposed entry:

"**New module-help.csv entry:**
```
{new row}
```

**Confirm?** [Y/N]"

If Y: Write the updated CSV.
If N: Adjust per feedback.

If the file doesn't exist, create it with a header row and the new entry.

### 2. Update docs/workflows.md

Load `{workflowsDocFile}`.

"**Updating docs/workflows.md with {skillName}...**"

Add a new section following the existing documentation format. Based on the existing pattern in workflows.md:

```markdown
---

## {skillName}

**Workflow:** `{skillName}`

**Purpose:**
{skill purpose from concept}

**When to Use:**
{when to use description}

**Key Steps:**
{numbered list of key steps from the SKILL.md flow}

**Pipeline:** add-forge-skill -> build-forge-skill -> build-forge-agent

**Agent(s):** Forge Builder (Morgan)
```

Present the proposed section:

"**New docs/workflows.md section:**

{display the section}

**Confirm?** [Y/N]"

If Y: Append to workflows.md.
If N: Adjust per feedback.

Also update the workflow count at the top of the file if it mentions a count (e.g., "forge includes N workflows").

### 3. Present Update Summary

"**Module artifacts updated:**

- module-help.csv: New entry added for {skillName}
- docs/workflows.md: New section added for {skillName}
- Workflow count updated: {old count} -> {new count}"

### 4. Update Output File

Append to `{outputFile}`:

```markdown
---

## Module Artifacts Updated

**module-help.csv:** Entry added
**docs/workflows.md:** Section added, count updated from {old} to {new}
```

### 5. Present MENU OPTIONS

Display: **Artifacts updated. Select an option:** [C] Continue to Validation

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

#### Menu Handling Logic:

- IF C: Update {outputFile} frontmatter with stepsCompleted, then load, read entire file, then execute {nextStepFile}
- IF Any other: help user respond, then [Redisplay Menu Options](#5-present-menu-options)

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- module-help.csv updated with new skill entry
- docs/workflows.md updated with new workflow section
- Workflow count updated if applicable
- Existing entries preserved exactly
- User confirmed changes before application
- stepsCompleted updated

### ❌ SYSTEM FAILURE:

- Modifying or removing existing entries
- Not matching the existing documentation format
- Applying changes without user confirmation
- Forgetting to update the workflow count
- Modifying files not in scope (SKILL.md, agent specs)

**Master Rule:** Only ADD new entries. Preserve all existing content exactly. Skipping steps is FORBIDDEN.
