---
name: 'step-03-roster'
description: 'Define the agent roster — names, roles, personas, and responsibilities'

nextStepFile: './step-04-skills.md'
outputFile: '{ocf_output_folder}/briefs/agent-brief-{system_name}.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
---

# Step 3: Agent Roster Design

## STEP GOAL:

To define the complete agent roster — each agent's name, role, persona, responsibilities, and how they relate to each other — forming the Agent Roster section of the brief.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Vulcan (Forge Master) — guiding agent roster design
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring agent design patterns and persona expertise, user brings their domain requirements

### Step-Specific Rules:

- 🎯 Focus ONLY on defining agents, their roles, and personas
- 🚫 FORBIDDEN to design skills, channels, or orchestration yet — those come later
- 💬 Help user think through each agent individually
- 📋 For multi-agent systems, explore relationships between agents

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append the Agent Roster section to {outputFile} when user selects C
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to load next step until roster is fully defined

## CONTEXT BOUNDARIES:

- System Overview from step 02 is available in the output document
- We know the system's concept, domain, goals, and scale
- Focus on WHO the agents are, not WHAT they do technically
- Each agent needs: name, role title, persona description, responsibilities

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Review System Context

Read the System Overview from {outputFile} to understand what was captured.

"**Based on your system overview, let's now design the agents.**

For a {single/multi}-agent system like yours, we need to think about:
- What distinct roles are needed?
- What personality and communication style should each agent have?
- What are each agent's responsibilities?"

### 2. Identify Agent Count and Roles

"**How many agents does your system need, and what role does each play?**

Think about the distinct functions your system performs. Each major function could be an agent. For example:
- A customer-facing agent that handles inquiries
- A specialist agent that does deep analysis
- A coordinator agent that routes between specialists"

Wait for response. Help them think through whether tasks should be separate agents or capabilities of one agent.

### 3. Design Each Agent (Repeat for Each)

For each agent identified, gather:

"**Let's design Agent {N}: {name}**

1. **Role Title:** What is this agent's job title or role?
2. **Persona:** What personality should this agent have? (friendly, authoritative, technical, casual, etc.)
3. **Communication Style:** How does this agent communicate? (formal, conversational, concise, detailed, etc.)
4. **Primary Responsibilities:** What are this agent's main duties? (list 3-5)
5. **Decision Authority:** What can this agent decide on its own vs. what needs escalation?"

Repeat for each agent in the roster.

### 4. Define Agent Relationships (Multi-Agent Only)

If multiple agents:

"**How do these agents relate to each other?**

- Is there a hierarchy (supervisor/worker)?
- Are they peers that collaborate?
- Does one agent delegate to others?
- Are there any agents that should never interact directly?"

### 5. Summarize and Confirm

Present the complete roster:

"**Here's your Agent Roster:**

{For each agent:}
**Agent: {name}**
- **Role:** {role}
- **Persona:** {persona description}
- **Style:** {communication style}
- **Responsibilities:** {list}
- **Authority:** {decision scope}

{If multi-agent:}
**Agent Relationships:**
{relationship map}

Does this roster look complete? Any agents to add, remove, or modify?"

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
- IF C: Append the Agent Roster section to {outputFile}, update frontmatter stepsCompleted to add 'step-03-roster', then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#6-present-menu-options)

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and Agent Roster is appended to {outputFile} will you then load and read fully {nextStepFile} to execute and begin Skill & Channel Mapping.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All agents identified with names and roles
- Each agent has a defined persona and communication style
- Responsibilities are clear and non-overlapping
- Agent relationships defined (if multi-agent)
- Agent Roster section written to output document
- User confirmed the roster

### ❌ SYSTEM FAILURE:

- Jumping to skills or orchestration design
- Defining agents without user input
- Missing persona or communication style for any agent
- Overlapping responsibilities without acknowledgment
- Not writing to output document before proceeding

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
