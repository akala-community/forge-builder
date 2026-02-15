---
name: 'step-01-init'
description: 'Initialize workflow, discover agent brief, validate, and create workspace plan'

nextStepFile: './step-02-identity.md'
outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'
continueFile: './step-01b-continue.md'
moduleInputFolder: '{ocf_output_folder}/briefs'
inputFilePatterns:
  - 'agent-brief-*.md'
---

# Step 1: Initialize & Load Brief

## STEP GOAL:

To discover and load the agent system brief, validate its structure, extract the agent roster and system name, and create the workspace plan document that tracks all generation progress.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are an OpenClaw workspace generator preparing to build a complete agent system
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring expertise in OCF workspace assembly, user brings their agent system vision

### Step-Specific Rules:

- 🎯 Focus only on discovering, loading, and validating the agent brief
- 🚫 FORBIDDEN to generate any agent artifacts yet — that starts in step 02
- 💬 Approach: Systematic discovery and validation of the brief
- 📋 Extract and present the agent roster clearly before proceeding

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Create workspace-plan.md at {outputFile} with extracted brief data
- 📖 Track progress via stepsCompleted in workspace-plan.md frontmatter
- 🚫 FORBIDDEN to proceed without a valid brief loaded and validated

## CONTEXT BOUNDARIES:

- Available context: OCF module configuration, brief output folder location
- Focus: Brief discovery, validation, and workspace plan creation
- Limits: Do NOT generate any agent artifacts — only extract and organize brief data
- Dependencies: Requires create-agent-brief workflow to have been run first

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Check for Existing Workspace Plan

Check if {outputFile} already exists.

- **If exists AND has `stepsCompleted` with entries:** This is a continuation. Load, read entirely, then execute {continueFile}
- **If not found:** Continue to step 2 below

### 2. Discover Agent Brief

Search {moduleInputFolder} for files matching {inputFilePatterns}.

**If briefs found:**

"**Found the following agent system briefs:**

[1] {filename} ({date modified})
[2] {filename} ({date modified})
...

Which brief would you like to use? Enter the number, or provide a path to a different brief."

**If no briefs found:**

"**No agent system briefs found in {moduleInputFolder}.**

You need to run the **create-agent-brief** workflow first to generate a brief, or provide the path to an existing brief file.

**Path:**"

Wait for user to provide a path.

### 3. Load and Validate Brief

Load the selected brief file completely. Validate it contains:

- **Concept section** — high-level goals and idea
- **Agent Roster section** — roles, personas, and responsibilities
- **Skill & Channel Mapping section** — tools and bindings
- **Orchestration section** — communication patterns, routing, handoffs
- **Memory & Resilience section** — architecture, self-correction, safety

**If validation fails:**

"**Warning:** The brief appears to be missing the following sections: {missing sections}

This may result in incomplete artifact generation. Would you like to:
- [P] Proceed anyway
- [R] Provide a different brief"

Wait for user input.

### 4. Extract System Data

From the validated brief, extract:

- **System name** (from brief title or concept section)
- **Agent roster** — for each agent:
  - Agent name (kebab-case identifier)
  - Display name
  - Role/archetype
  - Key responsibilities
  - Assigned skills/channels
- **Architecture context** — orchestration patterns, memory architecture, resilience requirements
- **System-level requirements** — tool policies, logging, monitoring needs

### 5. Create Workspace Plan Document

Create {outputFile} with the following structure:

```markdown
---
stepsCompleted: ['step-01-init']
lastStep: 'step-01-init'
lastContinued: '{current_date}'
date: '{current_date}'
user_name: '{user_name}'
system_name: '{extracted_system_name}'
agent_count: {number_of_agents}
source_brief: '{path_to_brief}'
---

# Workspace Plan: {System Display Name}

## Source Brief
**Path:** {brief_path}
**System Name:** {system_name}
**Created:** {date}

## Agent Roster

### {Agent 1 Display Name} ({agent-1-kebab-name})
**Role:** {role}
**Responsibilities:** {responsibilities}
**Skills:** {skill list}

### {Agent 2 Display Name} ({agent-2-kebab-name})
...

## Architecture Context

### Orchestration
{orchestration patterns from brief}

### Memory Architecture
{memory architecture from brief}

### Resilience
{resilience requirements from brief}

## Generation Progress

| Step | Status | Artifacts |
|------|--------|-----------|
| 01 - Init | ✅ Complete | workspace-plan.md |
| 02 - Identity | ⬜ Pending | SOUL.md, AGENTS.md per agent |
| 03 - Context | ⬜ Pending | USER.md, MEMORY.md per agent |
| 04 - Skills | ⬜ Pending | skills/ directory per agent |
| 05 - Config | ⬜ Pending | openclaw.json, tool policies, memory, failover, heartbeat, logging |
| 06 - Self-Correction | ⬜ Pending | REVIEW.md per agent |
| 07 - Assembly | ⬜ Pending | Complete directory structure |
| 08 - Review | ⬜ Pending | User approval |
```

### 6. Present Summary

"**Workspace plan created successfully.**

**System:** {system_name}
**Agents:** {count} agents identified
**Brief:** {brief_path}

**Agent Roster:**
{list each agent with role}

**Next:** Identity Generation — generating SOUL.md and AGENTS.md for each agent.

**Proceeding to identity generation...**"

### 7. Present MENU OPTIONS

Display: **Select:** [C] Continue to Identity Generation

#### Menu Handling Logic:

- IF C: Save workspace plan to {outputFile}, update frontmatter stepsCompleted, then load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then [Redisplay Menu Options](#7-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and workspace-plan.md has been created with valid brief data will you then load and read fully `{nextStepFile}` to execute identity generation.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Agent brief discovered and loaded completely
- Brief validated for required sections
- System name, agent roster, and architecture context extracted
- workspace-plan.md created at {outputFile} with complete extracted data
- Generation progress table initialized
- Frontmatter stepsCompleted updated

### ❌ SYSTEM FAILURE:

- Proceeding without loading a valid brief
- Not validating brief sections
- Missing agents from roster extraction
- Not creating workspace-plan.md
- Generating artifacts in this step (too early)
- Not updating frontmatter stepsCompleted

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
