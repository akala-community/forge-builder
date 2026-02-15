---
name: 'step-03-communication'
description: 'Design spawn/send communication patterns and session routing between agents'

nextStepFile: './step-04-bindings.md'
outputFile: '{ocf_output_folder}/orchestration-design-{project_name}.md'
communicationReference: '../data/communication-mechanisms.md'
orchestrationReference: '../data/openclaw-orchestration-reference.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
---

# Step 3: Communication Design

**Progress: Step 3 of 7** — Next: Channel Bindings

## STEP GOAL:

Design the communication patterns between agents -- which agents spawn subagents, which use sessions_send for inter-agent messaging, what session routing looks like, and how the message flow works end-to-end.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a systems architect designing communication infrastructure
- ✅ If you already have been given a name, communication_style and persona, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring deep knowledge of OpenClaw's session tools — reference {communicationReference} and {orchestrationReference} for syntax

### Step-Specific Rules:

- 🎯 Focus only on agent-to-agent communication — not channel bindings (Step 4)
- 🚫 FORBIDDEN to design channel routing in this step
- 💬 Approach: For each agent relationship from the map, determine the communication mechanism
- 📋 Use the decision framework from {communicationReference} to guide spawn vs send choices

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append the Communication Patterns section to {outputFile} when complete
- 📖 Update frontmatter stepsCompleted to add this step when completed
- 🚫 FORBIDDEN to load next step until user selects 'C'

## CONTEXT BOUNDARIES:

- Available context: Agent Map from Step 2 (relationships, roles, ids)
- Focus: Spawn/send patterns, session routing, message flow
- Limits: Don't configure channel bindings — that's Step 4
- Dependencies: Agent relationships from Step 2

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Review Agent Relationships

Present the relationships from Step 2 that need communication patterns (delegation, supervision, collaboration, reporting). Ask: for each, should it be **spawn** or **send**?

### 2. Explain Communication Mechanisms

Using {communicationReference}, explain the two mechanisms and the decision framework. Help the user understand the trade-offs before making decisions.

### 3. Design Each Communication Pattern

For each agent relationship, collaboratively determine the mechanism (spawn/send), trigger, data flow, and sync/async nature. Ask 1-2 questions per relationship, offer a recommendation, then confirm.

Build a communication pattern table: From, To, Mechanism, Trigger, Data Flow, Sync/Async.

### 4. Design Session Routing

Discuss session routing — which agents share context, any special routing needs, group chat participation. Reference session key patterns from {communicationReference}.

### 5. Cross-Agent Spawn Permissions

For any cross-agent spawns identified, determine the allowAgents configuration. Reference {communicationReference} for the config syntax.

### 6. Agent-to-Agent Messaging Config

For agents using sessions_send, configure the agentToAgent settings and ping-pong limits. Reference {communicationReference} for config syntax.

### 7. Assemble Communication Patterns Section

Compile into the output document section with: communication table, message flow diagram (text-based), cross-agent spawn permissions config, agent-to-agent messaging config, and session routing notes.

Present for review — every relationship from the agent map should be covered.

### 8. Present MENU OPTIONS

Display: "**Select an Option:** [A] Advanced Elicitation [C] Continue"

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF C: Append Communication Patterns section to {outputFile}, update frontmatter (add 'step-03-communication' to stepsCompleted), then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#8-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [C continue option] is selected and [Communication Patterns section appended to output file with frontmatter updated], will you then load and read fully `{nextStepFile}` to begin channel binding design.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Every agent relationship has a defined communication mechanism (spawn or send)
- Spawn vs send choice is justified for each relationship
- Cross-agent spawn permissions are documented
- Agent-to-agent messaging config is defined (if send is used)
- Communication table and flow diagram are clear
- Session routing is addressed
- User reviewed and approved patterns

### ❌ SYSTEM FAILURE:

- Leaving agent relationships without defined communication mechanisms
- Not explaining spawn vs send trade-offs
- Forgetting cross-agent spawn permissions
- Not enabling agent-to-agent messaging for send patterns
- Designing channel bindings (that's Step 4)

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
