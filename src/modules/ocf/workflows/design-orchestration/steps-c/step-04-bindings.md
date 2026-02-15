---
name: 'step-04-bindings'
description: 'Configure channel-to-agent routing bindings for all channels in the system'

nextStepFile: './step-05-failure.md'
outputFile: '{ocf_output_folder}/orchestration-design-{project_name}.md'
bindingReference: '../data/binding-syntax-reference.md'
orchestrationReference: '../data/openclaw-orchestration-reference.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
---

# Step 4: Channel Bindings

**Progress: Step 4 of 7** — Next: Failure Handling

## STEP GOAL:

Configure the channel-to-agent routing bindings that determine which agent handles inbound messages from each channel, account, peer, and group.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a systems architect configuring message routing
- ✅ If you already have been given a name, communication_style and persona, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring deep knowledge of OpenClaw's binding system — reference {bindingReference} and {orchestrationReference} for syntax and priority rules

### Step-Specific Rules:

- 🎯 Focus only on channel bindings — not failure handling (Step 5)
- 🚫 FORBIDDEN to design failure patterns in this step
- 💬 Approach: Walk through each channel and determine which agent handles it
- 📋 Use {bindingReference} for binding syntax, priority rules, and config examples

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append the Channel Bindings section to {outputFile} when complete
- 📖 Update frontmatter stepsCompleted to add this step when completed
- 🚫 FORBIDDEN to load next step until user selects 'C'

## CONTEXT BOUNDARIES:

- Available context: Agent Map (Step 2) and Communication Patterns (Step 3)
- Focus: Inbound message routing via bindings
- Limits: Don't design failure handling — that's Step 5
- Dependencies: Agent ids from Step 2, channel requirements from inputs

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Identify All Channels

Ask which channels the system will use (WhatsApp, Telegram, Discord, Signal, iMessage, Slack, Webchat). For each channel: how many accounts, which agents handle it, any per-peer overrides?

### 2. Explain Binding Priority

Using {bindingReference}, explain the most-specific-wins matching order so the user understands how routing decisions work.

### 3. Design Bindings Per Channel

For each channel, collaboratively determine: default routing agent, per-account routing (if multiple accounts), per-peer overrides (specific DMs/groups), and group chat mention configuration. Reference {bindingReference} for binding syntax.

### 4. Design DM Split (If Applicable)

If multiple people share a single channel account, discuss per-sender binding using peer matching. Reference {bindingReference} for DM split syntax.

### 5. Group Chat Mention Gating

For agents in group chats, determine mention patterns and whether agents respond to all messages or only when mentioned. Reference {bindingReference} for mention config syntax.

### 6. Channel Access Control

Discuss DM policy (allowlist vs open) and group policies for channels that support access control. Reference {bindingReference} for access control config.

### 7. Assemble Channel Bindings Section

Compile into the output document section with: channels used table, complete bindings array (ordered by specificity), group chat configuration, access control policies, and binding priority order explanation.

Present for review — test mentally: "If a message comes from {source}, which agent handles it?"

### 8. Present MENU OPTIONS

Display: "**Select an Option:** [A] Advanced Elicitation [C] Continue"

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF C: Append Channel Bindings section to {outputFile}, update frontmatter (add 'step-04-bindings' to stepsCompleted), then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#8-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [C continue option] is selected and [Channel Bindings section appended to output file with frontmatter updated], will you then load and read fully `{nextStepFile}` to begin failure handling design.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Every channel has defined routing to an agent
- Bindings are ordered by specificity (most specific first)
- Per-account and per-peer overrides are documented
- Group chat mention gating is configured
- Access control policies are defined
- User has verified the priority order makes sense

### ❌ SYSTEM FAILURE:

- Channels without defined agent routing
- Bindings in wrong priority order
- Missing group chat mention configuration
- Not explaining binding priority rules
- Starting failure handling design (that's Step 5)

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
