---
name: 'step-04-register-skill'
description: 'Update forge-builder.spec.md to register the new skill as a build target'

nextStepFile: './step-05-update-artifacts.md'
outputFile: '{forge_artifacts}/add-skill-context.md'
forgeBuilderSpecFile: '{project-root}/src/modules/forge/agents/forge-builder.spec.md'
forgeSpecFile: '{project-root}/src/modules/forge/agents/forge.spec.md'
---

# Step 4: Register in Forge Builder

## STEP GOAL:

Update the Forge Builder (Morgan) agent specification to register the new skill as a build target in the command table, and optionally update The Forge's agent specification to include the new skill in its command table.

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
- ✅ Precise and careful when modifying agent specifications
- ✅ You understand the command table format and trigger code conventions
- ✅ User confirms changes before they are applied

### Step-Specific Rules:

- 🎯 Focus ONLY on registering the skill in agent spec command tables
- 🚫 FORBIDDEN to modify the SKILL.md (that was step-03)
- 💬 Present proposed changes for user review before applying
- 📋 Preserve existing command table entries exactly — only ADD the new entry

## EXECUTION PROTOCOLS:

- 🎯 Load current forge-builder.spec.md and forge.spec.md
- 💾 Add new command table entries for the skill
- 📖 Update {outputFile} frontmatter stepsCompleted when registration is complete
- 🚫 FORBIDDEN to remove or modify existing command table entries

## CONTEXT BOUNDARIES:

- Available: Skill concept from step-01, generated SKILL.md from step-03
- Focus: Add the new skill to both agent command tables
- Limits: Only modify command tables — no other changes to agent specs
- Dependencies: step-03 must be complete (SKILL.md written)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Read Current Forge Builder Spec

Load `{forgeBuilderSpecFile}` and locate the "Planned Commands" table.

"**Registering {skillName} in the Forge Builder pipeline.**"

Identify:
- Current command table entries
- Used trigger codes (2-letter codes)
- Available trigger code for the new skill

### 2. Read Current Forge Spec

Load `{forgeSpecFile}` and locate the "Planned Commands" table.

Identify:
- Current command table entries
- Used trigger codes
- Whether the new skill should appear in The Forge's command table (it should if it's a user-facing skill)

### 3. Propose Forge Builder Registration

"**Proposed changes to forge-builder.spec.md:**

Adding new entry to the Planned Commands table:

| Trigger | Command | Description | Workflow |
|---------|---------|-------------|----------|
| {trigger-code} | {skillName} | {skill description} | {skillName} |

**Full updated command table:**
{show complete table with new entry added in logical position}

**Confirm these changes?** [Y/N]"

If N: Adjust trigger code or description per user feedback.

### 4. Propose Forge Registration (If Applicable)

If the new skill is user-facing (The Forge activates it at runtime):

"**Proposed changes to forge.spec.md:**

Adding new entry to the Planned Commands table:

| Trigger | Command | Description | Workflow |
|---------|---------|-------------|----------|
| {trigger-code} | {skillName} | {skill description} | {skillName} |

**Full updated command table:**
{show complete table with new entry added in logical position}

**Confirm these changes?** [Y/N]"

If N: Adjust per user feedback.

If the skill is build-only (not user-facing): Skip this step and note it.

### 5. Apply Changes

Once user confirms:

Update `{forgeBuilderSpecFile}`:
- Add the new command table entry in the correct position
- Preserve all existing entries exactly

If applicable, update `{forgeSpecFile}`:
- Add the new command table entry in the correct position
- Preserve all existing entries exactly

"**Registration complete.**
- forge-builder.spec.md: Updated with {skillName}
- forge.spec.md: {Updated / Not updated (build-only skill)}"

### 6. Update Output File

Append to `{outputFile}`:

```markdown
---

## Registration Complete

**Forge Builder (Morgan):**
- Trigger: {trigger-code}
- Command: {skillName}
- Added to command table: Yes

**The Forge:**
- Added to command table: {Yes/No — build-only skill}
- Trigger: {trigger-code or N/A}
```

### 7. Present MENU OPTIONS

Display: **Skill registered. Select an option:** [C] Continue to Module Artifact Updates

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

#### Menu Handling Logic:

- IF C: Update {outputFile} frontmatter with stepsCompleted, then load, read entire file, then execute {nextStepFile}
- IF Any other: help user respond, then [Redisplay Menu Options](#7-present-menu-options)

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Forge Builder command table updated with new skill entry
- The Forge command table updated (if user-facing skill)
- Trigger codes don't conflict with existing entries
- Existing command table entries preserved exactly
- User confirmed changes before application
- stepsCompleted updated

### ❌ SYSTEM FAILURE:

- Modifying or removing existing command table entries
- Using a trigger code that conflicts with an existing entry
- Applying changes without user confirmation
- Modifying parts of the spec beyond the command table
- Not preserving exact formatting of existing entries

**Master Rule:** Only ADD entries to command tables. Never modify or remove existing entries. Skipping steps is FORBIDDEN.
