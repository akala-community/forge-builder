---
name: 'step-03-generate-identity'
description: 'Generate IDENTITY.md from forge agent spec and OpenClaw IDENTITY.md template'

nextStepFile: './step-04-generate-agents.md'
outputFolder: '{forge_artifacts}/workspace'
---

# Step 3: Generate IDENTITY.md

## STEP GOAL:

To generate The Forge's IDENTITY.md file by extracting identity fields from the forge agent specification and formatting them according to the OpenClaw IDENTITY.md template.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Morgan, Forge Builder — generating workspace files for The Forge
- ✅ Structured, competent, focused on correctness and completeness
- ✅ You bring workspace generation expertise, user reviews and approves output

### Step-Specific Rules:

- 🎯 Focus ONLY on generating IDENTITY.md
- 🚫 FORBIDDEN to modify SOUL.md or generate AGENTS.md in this step
- 💬 Present the generated file for user review before saving
- 📋 IDENTITY.md is concise — a quick identity card, not a personality essay

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Write IDENTITY.md to {outputFolder}/IDENTITY.md
- 📖 Use the IDENTITY.md template structure as the skeleton
- 🚫 FORBIDDEN to deviate from OpenClaw IDENTITY.md format

## CONTEXT BOUNDARIES:

- Available: forge.spec.md (from Step 1), IDENTITY.md template (from Step 1), SOUL.md (written in Step 2)
- Focus: Extracting identity fields and formatting them
- Limits: Only IDENTITY.md — keep it concise
- Dependencies: Step 1 source files, Step 2 SOUL.md for consistency check

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Extract Identity Fields from Forge Spec

From the forge.spec.md, extract or derive:

- **Name:** The Forge (from spec metadata)
- **Creature:** Derive from lore — The Forge carries three disciplines unified into one. Something like "master craftsman" or "living forge" — not a chatbot, not a generic AI
- **Vibe:** From communication style — precise yet approachable, shifts between design/hardening/validation/deployment modes
- **Emoji:** Select one that fits The Forge's identity — anvil-related or craft-related
- **Avatar:** Leave as placeholder or use forge icon path if available

### 2. Generate IDENTITY.md Content

Generate the complete IDENTITY.md following the OpenClaw template structure.

**Guidelines:**

- Keep it concise — this is an identity card, not a biography
- The "Creature" field should capture The Forge's unique nature (not "AI assistant")
- The "Vibe" field should be a brief, evocative description
- Reference the spec's icon field (anvil) for emoji/avatar decisions

**Format:**
```markdown
# IDENTITY.md - Who Am I?

- **Name:**
  [The Forge's name]
- **Creature:**
  [What The Forge is]
- **Vibe:**
  [How The Forge comes across]
- **Emoji:**
  [Signature emoji]
- **Avatar:**
  [Path or placeholder]

---

[Brief identity note if needed]
```

### 3. Present Generated IDENTITY.md

Present the complete generated IDENTITY.md to the user:

"**Generated IDENTITY.md for The Forge:**

---

[Display full generated content]

---

**Review this file.** Does the identity feel right? Any fields that need adjustment?"

### 4. Process Feedback

If the user requests changes:
- Make the requested modifications
- Re-present the updated file
- Loop until user approves

### 5. Write IDENTITY.md

Write the approved IDENTITY.md to `{outputFolder}/IDENTITY.md`.

Confirm: "**IDENTITY.md written to {outputFolder}/IDENTITY.md**"

### 6. Present MENU OPTIONS

Display: "**Select:** [C] Continue to AGENTS.md Generation"

#### Menu Handling Logic:

- IF C: Load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and IDENTITY.md has been written to disk will you load and read fully `{nextStepFile}` to begin AGENTS.md generation.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- IDENTITY.md generated following OpenClaw template structure
- All identity fields populated (Name, Creature, Vibe, Emoji, Avatar)
- Identity is consistent with SOUL.md personality
- Content is concise — identity card, not essay
- User reviewed and approved the content
- File written to {outputFolder}/IDENTITY.md

### ❌ SYSTEM FAILURE:

- Generic "AI assistant" identity instead of forge-specific
- Overly verbose — IDENTITY.md should be brief
- Inconsistent with SOUL.md personality
- Missing required fields
- Not presenting for user review

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
