---
name: 'step-02-agent-map'
description: 'Map all agents in the system, their roles, and their relationships to each other'

nextStepFile: './step-03-communication.md'
outputFile: '{ocf_output_folder}/orchestration-design-{project_name}.md'
orchestrationReference: '../data/openclaw-orchestration-reference.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
---

# Step 2: Agent Map

**Progress: Step 2 of 7** — Next: Communication Design

## STEP GOAL:

Map all agents in the system — their ids, roles, responsibilities, relationships, and boundaries — to create the foundation that all subsequent orchestration design steps build upon.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a systems architect mapping the agent landscape
- ✅ If you already have been given a name, communication_style and persona, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring OpenClaw multi-agent expertise, user brings their system requirements

### Step-Specific Rules:

- 🎯 Focus only on mapping agents and relationships — no communication pattern design yet
- 🚫 FORBIDDEN to design spawn/send patterns in this step — that's Step 3
- 💬 Approach: Walk through each agent systematically, asking about purpose and boundaries
- 📋 Reference {orchestrationReference} for agent definition syntax

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append the Agent Map section to {outputFile} when complete
- 📖 Update frontmatter stepsCompleted to add this step when completed
- 🚫 FORBIDDEN to load next step until user selects 'C'

## CONTEXT BOUNDARIES:

- Available context: Input documents loaded in Step 1, agent brief if available
- Focus: Agent identity, roles, and relationships only
- Limits: Don't design communication patterns or channel bindings yet
- Dependencies: Agent roster from input documents (Step 1)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Review Discovered Agents

Present what was found from Step 1 inputs and ask user to confirm or start fresh if no agents were discovered.

### 2. Define Each Agent

For each agent, collaboratively define: `id` (lowercase, no spaces), `name`, `role` (one sentence), `workspace`, `model` (if different from default), and whether it's the `default` agent.

Walk through each agent one at a time — ask 1-2 questions per agent, confirm, then move to the next.

### 3. Map Agent Relationships

Explore how agents relate to each other. Relationship types to consider:
- **Supervises:** Agent A oversees Agent B's work
- **Delegates to:** Agent A sends tasks to Agent B
- **Collaborates with:** Agent A and Agent B work together
- **Reports to:** Agent A sends results back to Agent B
- **Independent:** Agent operates in isolation

Build a relationship matrix from the discussion.

### 4. Identify the Default Agent

Discuss which agent should be the default — the one that handles messages when no specific binding matches. Present candidates with brief descriptions.

### 5. Assemble Agent Map Section

Compile the agent map into the output document section with: agent roster table (ID, Name, Role, Model, Default), agent relationships matrix, agent count, and default agent ID.

Present the completed agent map for user review. Ask if anything needs to be added, modified, or removed.

### 6. Present MENU OPTIONS

Display: "**Select an Option:** [A] Advanced Elicitation [C] Continue"

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF C: Append Agent Map section to {outputFile}, update frontmatter (add 'step-02-agent-map' to stepsCompleted), then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#6-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [C continue option] is selected and [Agent Map section appended to output file with frontmatter updated], will you then load and read fully `{nextStepFile}` to begin communication pattern design.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Every agent has a defined id, name, and role
- Agent relationships are mapped
- Default agent is identified
- Agent map section written to output document
- Frontmatter updated with step completion
- User reviewed and approved the agent map

### ❌ SYSTEM FAILURE:

- Not defining agent ids (needed for bindings and config)
- Skipping relationship mapping
- Not identifying a default agent
- Starting to design communication patterns (that's Step 3)
- Proceeding without user review

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
