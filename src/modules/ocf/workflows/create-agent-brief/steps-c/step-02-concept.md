---
name: 'step-02-concept'
description: 'Capture the agent system concept, domain, and high-level goals'

nextStepFile: './step-03-roster.md'
outputFile: '{ocf_output_folder}/briefs/agent-brief-{system_name}.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
---

# Step 2: Concept Gathering

## STEP GOAL:

To capture the user's agent system concept, domain, high-level goals, target users, and the problem the system solves — forming the System Overview section of the brief.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Vulcan (Forge Master) — guiding discovery of the agent system concept
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring agent system architecture expertise, user brings their domain knowledge and vision

### Step-Specific Rules:

- 🎯 Focus ONLY on capturing the system concept, domain, and goals
- 🚫 FORBIDDEN to design agents, skills, or architecture yet — that comes in later steps
- 💬 Use open-ended questions to draw out the user's vision
- 📋 Ask 1-2 questions at a time, think about responses before continuing

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append the System Overview section to {outputFile} when user selects C
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to load next step until concept is fully captured

## CONTEXT BOUNDARIES:

- Step 01 created the output document with initial frontmatter
- We have the system name from initialization
- Focus on the BIG PICTURE — what the system does, why it exists, who it serves
- Do NOT get into implementation details yet

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Open the Concept Discussion

"**Let's start by understanding your agent system at a high level.**

Tell me about the system you want to build. What problem does it solve? What does it do?"

Wait for user response. Think about their answer before continuing.

### 2. Explore the Domain

Based on their response, explore:

"**What domain or industry does this system operate in?**

Understanding the domain helps us design agents with the right expertise and communication style."

### 3. Identify Target Users

"**Who will interact with this system?**

Think about:
- End users (customers, employees, etc.)
- Administrators or operators
- Other systems that integrate with it"

### 4. Clarify Goals and Success Criteria

"**What does success look like for this system?**

- What are the primary goals?
- What outcomes should it produce?
- How will you measure if it's working well?"

### 5. Determine Scale and Complexity

"**Let's understand the scale:**

- Is this a single-agent or multi-agent system?
- How many concurrent users or requests do you expect?
- Are there specific performance or availability requirements?"

### 6. Summarize and Confirm

Present a summary of everything gathered:

"**Here's what I've captured for your System Overview:**

**System Name:** {system_name}
**Domain:** {domain}
**Problem Statement:** {problem}
**Target Users:** {users}
**Primary Goals:** {goals}
**Scale:** {single/multi-agent, expected load}
**Success Criteria:** {criteria}

Does this accurately capture your vision? Any adjustments?"

Refine based on user feedback.

### 7. Present MENU OPTIONS

Display: **Select an Option:** [A] Advanced Elicitation [C] Continue

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu
- User can chat or ask questions - always respond and then redisplay the menu

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF C: Append the System Overview section to {outputFile}, update frontmatter stepsCompleted to add 'step-02-concept', then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#7-present-menu-options)

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and System Overview is appended to {outputFile} will you then load and read fully {nextStepFile} to execute and begin Agent Roster Design.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- System concept clearly articulated
- Domain and target users identified
- Goals and success criteria defined
- Scale and complexity understood
- System Overview section written to output document
- User confirmed the summary

### ❌ SYSTEM FAILURE:

- Jumping to agent design or technical architecture
- Not asking enough questions to understand the concept
- Writing the overview without user confirmation
- Proceeding without appending to output document

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
