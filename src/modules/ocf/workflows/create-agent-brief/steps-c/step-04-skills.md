---
name: 'step-04-skills'
description: 'Map skills, tools, and channel bindings per agent'

nextStepFile: './step-05-orchestration.md'
outputFile: '{ocf_output_folder}/briefs/agent-brief-{system_name}.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
---

# Step 4: Skill & Channel Mapping

## STEP GOAL:

To identify and map skills, tools, and channel bindings for each agent in the roster — forming the Skills & Channels section of the brief.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Vulcan (Forge Master) — guiding skill and channel architecture
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring OpenClaw skill/channel architecture expertise, user brings their integration requirements

### Step-Specific Rules:

- 🎯 Focus ONLY on skills, tools, and channels per agent
- 🚫 FORBIDDEN to design orchestration or memory architecture yet
- 💬 Walk through each agent's capabilities systematically
- 📋 Distinguish between built-in skills and custom skills needed

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append the Skills & Channels section to {outputFile} when user selects C
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to load next step until mapping is complete

## CONTEXT BOUNDARIES:

- System Overview and Agent Roster are available in the output document
- We know each agent's role, persona, and responsibilities
- Focus on WHAT each agent can DO and WHERE it communicates
- Skills = capabilities, Channels = communication endpoints

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Review Agent Roster

Read the Agent Roster from {outputFile} to understand each agent's role and responsibilities.

"**Now let's define what each agent can actually DO and WHERE it communicates.**

For each agent, we'll map:
- **Skills** — what capabilities does it have?
- **Tools** — what external tools or APIs does it use?
- **Channels** — where does it communicate? (WhatsApp, Telegram, Discord, API, etc.)"

### 2. Map Skills Per Agent (Repeat for Each)

For each agent in the roster:

"**Agent: {name} — Skills & Tools**

Based on {name}'s responsibilities ({list responsibilities}), what skills does this agent need?

Think about:
- **Conversational skills** (Q&A, guidance, support)
- **Processing skills** (data analysis, document generation, search)
- **Integration skills** (API calls, database queries, file operations)
- **Custom skills** specific to your domain

What tools or external services should this agent be able to use?"

### 3. Map Channels Per Agent (Repeat for Each)

For each agent:

"**Agent: {name} — Channel Bindings**

Where will {name} communicate? Select all that apply and add any others:

- WhatsApp
- Telegram
- Discord
- Slack
- Web Chat
- API endpoint
- Email
- SMS
- Custom channels

Does {name} need different behavior on different channels?"

### 4. Identify Shared vs. Unique Skills

"**Looking across all agents, are there:**

- **Shared skills** that multiple agents use? (These could be shared skill modules)
- **Unique skills** that only one agent needs?
- **Skills that need customization** per agent? (same base skill, different configuration)"

### 5. Summarize and Confirm

Present the complete skills and channels map:

"**Skills & Channels Map:**

{For each agent:}
**Agent: {name}**
- **Skills:** {list of skills}
- **Tools:** {list of external tools/APIs}
- **Channels:** {list of channel bindings}
- **Channel-specific behaviors:** {any differences per channel}

**Shared Skills:** {list}
**Custom Skills Needed:** {list of skills that need to be built}

Does this mapping look complete? Any skills or channels to add or modify?"

Refine based on feedback.

### 6. Present MENU OPTIONS

Display: **Select an Option:** [A] Advanced Elicitation [C] Continue

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu
- User can chat or ask questions - always respond and then redisplay the menu

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF C: Append the Skills & Channels section to {outputFile}, update frontmatter stepsCompleted to add 'step-04-skills', then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#6-present-menu-options)

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and Skills & Channels is appended to {outputFile} will you then load and read fully {nextStepFile} to execute and begin Orchestration Planning.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Every agent has skills mapped to their responsibilities
- Channel bindings defined for each agent
- Shared vs. unique skills identified
- Custom skills that need building are called out
- Skills & Channels section written to output document
- User confirmed the mapping

### ❌ SYSTEM FAILURE:

- Jumping to orchestration or memory design
- Assigning skills without tying them to responsibilities
- Missing channel bindings for any agent
- Not identifying custom skills that need development
- Not writing to output document before proceeding

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
