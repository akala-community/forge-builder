---
name: 'step-01-init'
description: 'Load all source files, validate inputs, present summary'

nextStepFile: './step-02-generate-soul.md'
forgeSpecFile: '{project-root}/src/modules/forge/agents/forge.spec.md'
soulTemplateFile: '{project-root}/docs/reference/templates/SOUL.md'
identityTemplateFile: '{project-root}/docs/reference/templates/IDENTITY.md'
agentsTemplateFile: '{project-root}/docs/reference/templates/AGENTS.md'
outputFolder: '{forge_artifacts}/workspace'
---

# Step 1: Initialize & Load Source Material

## STEP GOAL:

To load all source files required for workspace generation — the forge agent specification and OpenClaw workspace templates — validate they exist, and present a summary of loaded material.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Morgan, Forge Builder — Module Lifecycle Manager
- ✅ Structured, competent, focused on correctness and completeness
- ✅ You bring workspace generation expertise, user brings domain knowledge of The Forge

### Step-Specific Rules:

- 🎯 Focus ONLY on loading and validating source files
- 🚫 FORBIDDEN to generate any workspace files in this step
- 💬 Present a clear summary of everything loaded
- 📋 Validate all required inputs exist before proceeding

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Load all source files into context
- 📖 Validate each required file exists
- 🚫 FORBIDDEN to proceed if required files are missing

## CONTEXT BOUNDARIES:

- This is the first step — no prior context available
- Focus: Loading and validating source material only
- Limits: Do not generate any content yet
- Dependencies: None

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Forge Agent Specification

Load and read completely: `{forgeSpecFile}`

This is the primary source material containing:
- Agent persona (role, identity, communication style, principles)
- Three-master-craftsmen lore (Vulcan, Anima, Cog)
- Forge metaphors (forging, tempering, quality inspection, blueprints)
- Menu commands and workflow references

**If file not found:** Report error and halt. This file is required.

### 2. Load OpenClaw Workspace Templates

Load and read completely each template:
- `{soulTemplateFile}` — SOUL.md template (personality, behavioral guidelines)
- `{identityTemplateFile}` — IDENTITY.md template (identity card)
- `{agentsTemplateFile}` — AGENTS.md template (operational instructions)

**If any template not found:** Report which templates are missing and halt. All three templates are required.

### 3. Load Optional Module Context

Attempt to load these files for additional context (non-fatal if missing):
- `{project-root}/src/modules/forge/module.yaml`
- `{project-root}/src/modules/forge/README.md`
- `{project-root}/src/modules/forge/docs/agents.md`

Note which optional files were loaded for reference.

### 4. Create Output Directory

Ensure `{outputFolder}` exists. Create it if needed.

### 5. Present Source Summary

Present a summary of everything loaded:

"**Source Material Loaded Successfully**

---

**Agent Specification:** {forgeSpecFile}
- Name: [name from spec]
- Role: [role from spec]
- Identity Theme: [brief lore summary]
- Communication Style: [brief style summary]
- Menu Commands: [count] commands defined

**OpenClaw Templates:**
- SOUL.md template: [loaded/missing]
- IDENTITY.md template: [loaded/missing]
- AGENTS.md template: [loaded/missing]

**Optional Context:**
- [list of optional files loaded]

**Output Location:** {outputFolder}

---

**All required inputs validated. Ready to begin generating workspace files.**"

### 6. Present MENU OPTIONS

Display: "**Select:** [C] Continue to SOUL.md Generation"

#### Menu Handling Logic:

- IF C: Load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and all required source files have been validated will you load and read fully `{nextStepFile}` to begin SOUL.md generation.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- forge.spec.md loaded and read completely
- All 3 OpenClaw workspace templates loaded
- Optional context files loaded where available
- Output directory confirmed
- Clear summary presented to user
- User confirms readiness to proceed

### ❌ SYSTEM FAILURE:

- Not loading forge.spec.md
- Not loading all 3 workspace templates
- Generating workspace content in this step
- Proceeding without validating required inputs
- Not presenting summary to user

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
