---
name: 'step-01-init'
description: 'Initialize the orchestration design workflow by discovering inputs and setting up the output document'

nextStepFile: './step-02-agent-map.md'
outputFile: '{ocf_output_folder}/orchestration-design-{project_name}.md'
templateFile: '../templates/orchestration-design-template.md'
---

# Step 1: Workflow Initialization

**Progress: Step 1 of 7** — Next: Agent Map

## STEP GOAL:

Initialize the orchestration design workflow by discovering input documents (agent briefs, existing workspace configs), loading the output template, and preparing the user for the design process.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a systems architect and orchestration designer (Vulcan — Forge Master)
- ✅ If you already have been given a name, communication_style and persona, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring deep OpenClaw orchestration expertise, user brings their agent system requirements

### Step-Specific Rules:

- 🎯 Focus only on initialization and input discovery — no design work yet
- 🚫 FORBIDDEN to start designing orchestration patterns in this step
- 💬 Approach: Systematic setup with clear reporting to user
- 📋 Discover and load agent briefs, workspace files, existing configs

## EXECUTION PROTOCOLS:

- 🎯 Discover and load all relevant input documents
- 💾 Initialize output document from template with proper frontmatter
- 📖 Update frontmatter: add this step name to stepsCompleted
- 🚫 FORBIDDEN to load next step until user selects 'C' (Continue)

## CONTEXT BOUNDARIES:

- Available context: Variables from workflow.md are available
- Focus: Workflow initialization and document setup only
- Limits: Don't design orchestration patterns yet — that starts in Step 2
- Dependencies: Configuration loaded from workflow.md initialization

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Input Document Discovery

Discover and load context documents. Documents can be in the following locations:
- {ocf_output_folder}/**
- {output_folder}/**
- docs/**

Try to discover the following:

- **Agent Brief** (`*brief*.md`) — the primary input for orchestration design
- **Existing Workspace Files** (`*AGENTS.md`, `*openclaw.json*`) — if modifying an existing system
- **Agent Specifications** (`*agent*.spec.md`, `*agent*.md`) — individual agent definitions
- **Channel Documentation** (`*channel*`, `*binding*`) — existing channel configuration

**Loading Rules:**

- Load ALL discovered files completely (no offset/limit)
- Track all successfully loaded files in frontmatter `inputDocuments` array
- Prioritize agent briefs — they contain the roster and channel requirements

Confirm what you found with the user and ask if they want to provide anything else. Only after confirmation proceed to loading.

### 2. Assess Inputs

After loading inputs, assess what's available:

**Agent Roster Assessment:**
- How many agents are defined?
- Are roles and responsibilities clear?
- Any missing information?

**Channel Assessment:**
- Which channels are mentioned?
- Any existing binding configurations?
- DM vs group chat requirements?

**Existing Orchestration:**
- Any existing communication patterns to extend?
- Any existing openclaw.json to reference?

### 3. Create Output Document

**Document Setup:**

- Copy the template from `{templateFile}` to `{outputFile}`
- Initialize frontmatter with proper structure:
  - `stepsCompleted: ['step-01-init']`
  - `date: {current date}`
  - `user_name: {user_name}`
  - `project_name: {project_name}`
  - `agentCount: {discovered count}`
  - `channelCount: {discovered count}`
  - `inputDocuments: [list of loaded files]`

### 4. Present Initialization Results

Present a summary to the user covering: document setup (created {outputFile} from template), input documents discovered (agent briefs, workspace files, agent specs, channel docs with counts and load status), agent roster count, channel count, and any existing orchestration patterns found. Ask if they have additional documents or are ready to continue.

### 5. Present MENU OPTIONS

Display: "**[C] Continue** — Move to Agent Map (Step 2 of 7)"

#### Menu Handling Logic:

- IF C: Update output file frontmatter (add 'step-01-init' to stepsCompleted), then load, read entire file, then execute {nextStepFile}
- IF user provides additional files: Load them, update inputDocuments, redisplay report
- IF Any other comments or queries: help user respond then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [C continue option] is selected and [frontmatter properly updated with this step added to stepsCompleted and input counts], will you then load and read fully `{nextStepFile}` to begin agent mapping.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Input documents discovered and loaded
- Output document created from template with proper frontmatter
- Agent count and channel count identified
- User informed of discovered inputs
- Menu presented and user input handled correctly
- Frontmatter updated with step completion

### ❌ SYSTEM FAILURE:

- Not searching for input documents
- Creating document without proper template structure
- Not reporting discovered documents to user
- Starting orchestration design in this step
- Proceeding without user selecting 'C'

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
