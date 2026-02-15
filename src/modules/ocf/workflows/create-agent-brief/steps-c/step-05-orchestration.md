---
name: 'step-05-orchestration'
description: 'Design multi-agent communication, routing, and handoff patterns'

nextStepFile: './step-06-resilience.md'
outputFile: '{ocf_output_folder}/briefs/agent-brief-{system_name}.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
---

# Step 5: Orchestration Planning

## STEP GOAL:

To design the multi-agent communication patterns, routing logic, and handoff mechanisms — forming the Orchestration section of the brief.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Vulcan (Forge Master) — guiding orchestration architecture
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring multi-agent orchestration expertise, user brings their workflow requirements

### Step-Specific Rules:

- 🎯 Focus ONLY on orchestration — communication, routing, handoffs
- 🚫 FORBIDDEN to design memory or resilience yet
- 💬 Use concrete scenarios to explore orchestration patterns
- 📋 For single-agent systems, this step covers internal routing and decision logic

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append the Orchestration section to {outputFile} when user selects C
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to load next step until orchestration is designed

## CONTEXT BOUNDARIES:

- System Overview, Agent Roster, and Skills & Channels are in the output document
- We know who the agents are, what they do, and where they communicate
- Focus on HOW agents work together and HOW requests flow
- This is the connective tissue between agents

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Review Current Architecture

Read the output document to understand the system so far.

"**Now let's design how your agents work together.**

We know your agents and their capabilities. Now we need to define:
- How do requests get to the right agent?
- How do agents hand off to each other?
- What happens when an agent can't handle something?"

### 2. Define Routing Topology

"**What routing pattern fits your system best?**

Common patterns:
- **Hub-and-Spoke:** One coordinator routes to specialists
- **Pipeline:** Requests flow through agents in sequence
- **Peer-to-Peer:** Agents communicate directly as needed
- **Hierarchical:** Supervisors delegate to workers
- **Event-Driven:** Agents react to events/triggers

Which pattern (or combination) describes how your system should work?"

Explore their choice with follow-up questions.

### 3. Design Request Flow

"**Walk me through a typical request from start to finish.**

1. Where does the request come in? (which channel)
2. Which agent receives it first?
3. How does it decide what to do?
4. Does it need to involve other agents?
5. How does the response get back to the user?"

Work through 2-3 representative scenarios to cover different flows.

### 4. Define Handoff Mechanisms

"**When one agent needs to pass work to another, how should that happen?**

Consider:
- **Context passing:** What information transfers between agents?
- **Handoff signals:** How does an agent know to take over?
- **User notification:** Should users know when they're being transferred?
- **Fallback routing:** What happens if the target agent is unavailable?"

### 5. Design Error and Edge Case Handling

"**What happens when things don't go as planned?**

- What if no agent can handle a request?
- What if an agent gets stuck or loops?
- What if multiple agents try to respond?
- Is there a human escalation path?"

### 6. Summarize and Confirm

Present the orchestration design:

"**Orchestration Design:**

**Routing Topology:** {pattern}

**Request Flow:**
{flow diagram or description}

**Handoff Mechanisms:**
- Context passing: {approach}
- Handoff signals: {approach}
- User notification: {approach}

**Error Handling:**
- Unhandled requests: {approach}
- Agent failures: {approach}
- Human escalation: {approach}

Does this orchestration design capture how your system should work?"

Refine based on feedback.

### 7. Present MENU OPTIONS

Display: **Select an Option:** [A] Advanced Elicitation [C] Continue

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu
- User can chat or ask questions - always respond and then redisplay the menu

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF C: Append the Orchestration section to {outputFile}, update frontmatter stepsCompleted to add 'step-05-orchestration', then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#7-present-menu-options)

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and Orchestration is appended to {outputFile} will you then load and read fully {nextStepFile} to execute and begin Memory & Resilience planning.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Routing topology clearly defined
- Request flows mapped with concrete scenarios
- Handoff mechanisms specified
- Error and edge case handling designed
- Orchestration section written to output document
- User confirmed the design

### ❌ SYSTEM FAILURE:

- Designing orchestration without understanding agent roles
- Skipping error handling
- Not exploring concrete scenarios
- Missing handoff mechanisms
- Not writing to output document before proceeding

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
