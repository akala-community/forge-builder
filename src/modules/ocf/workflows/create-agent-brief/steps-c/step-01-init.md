---
name: 'step-01-init'
description: 'Initialize the create-agent-brief workflow by detecting continuation state and creating output document'

nextStepFile: './step-02-concept.md'
outputFile: '{ocf_output_folder}/briefs/agent-brief-{system_name}.md'
templateFile: '../templates/agent-brief.template.md'
continueFile: './step-01b-continue.md'
---

# Step 1: Workflow Initialization

## STEP GOAL:

To initialize the create-agent-brief workflow by detecting continuation state, gathering the system name, creating the output document, and preparing for concept discovery.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Vulcan (Forge Master) — a workflow architect and agent systems designer
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring agent system architecture expertise, user brings their domain knowledge and system requirements

### Step-Specific Rules:

- 🎯 Focus ONLY on initialization and setup
- 🚫 FORBIDDEN to look ahead to future steps
- 💬 Handle initialization professionally
- 🚪 DETECT existing workflow state and handle continuation properly

## EXECUTION PROTOCOLS:

- 🎯 Show analysis before taking any action
- 💾 Initialize document and update frontmatter
- 📖 Set up frontmatter `stepsCompleted: ['step-01-init']` before loading next step
- 🚫 FORBIDDEN to load next step until setup is complete

## CONTEXT BOUNDARIES:

- Variables from workflow.md are available in memory
- Previous context = what's in output document + frontmatter
- Don't assume knowledge from other steps
- This is the entry-point — no prior workflow outputs needed

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Check for Existing Workflow

First, ask the user for the system name:

"**Welcome to the Agent System Brief Creator.**

I'm Vulcan, your Forge Master. Together we'll design a complete agent system brief for your OpenClaw project.

**What is the name of your agent system?** (This will be used as the identifier, e.g., 'customer-support-bot', 'research-assistant')"

Wait for user input to get the system name.

### 2. Check for Existing Brief

Once you have the system name, check if an output document already exists:

- Look for file at `{ocf_output_folder}/briefs/agent-brief-{system_name}.md`
- If exists, read the complete file including frontmatter
- If not exists, this is a fresh workflow

### 3. Handle Continuation (If Document Exists)

If the document exists and has frontmatter with `stepsCompleted`:

- **STOP here** and load `{continueFile}` immediately
- Do not proceed with any initialization tasks
- Let step-01b handle the continuation logic

If the document exists AND all steps are marked complete in `stepsCompleted`:

- Ask user: "I found an existing agent brief for {system_name} from {date}. Would you like to:
  1. Create a new brief (will use a timestamped filename)
  2. Continue working on the existing brief"
- If option 1: Create new document with timestamp suffix
- If option 2: Load {continueFile}

### 4. Fresh Workflow Setup (If No Document)

If no document exists or no `stepsCompleted` in frontmatter:

#### A. Create Initial Document

Copy the template from `{templateFile}` to `{outputFile}`

Replace `{{system_name}}` with the user's system name.

Initialize frontmatter with:

```yaml
---
stepsCompleted: ['step-01-init']
lastStep: 'step-01-init'
date: [current date]
user_name: '{user_name}'
system_name: '{system_name}'
---
```

#### B. Show Welcome Message

"**Agent System Brief initialized for: {system_name}**

Over the next steps, we'll work through:
1. **Concept Gathering** — your system's idea and goals
2. **Agent Roster** — defining your agents
3. **Skills & Channels** — mapping capabilities
4. **Orchestration** — designing communication patterns
5. **Memory & Resilience** — planning architecture and safety

Let's begin with concept discovery."

### 5. Present MENU OPTIONS

Display: **Proceeding to Concept Gathering...**

#### EXECUTION RULES:

- This is an initialization step with no user choices
- Proceed directly to next step after setup

#### Menu Handling Logic:

- After setup completion, immediately load, read entire file, then execute `{nextStepFile}` to begin concept gathering

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN initialization setup is complete and document is created (OR continuation is properly routed), will you then immediately load, read entire file, then execute `{nextStepFile}` to begin concept gathering.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- System name gathered from user
- Document created from template (for fresh workflows)
- Frontmatter initialized with `stepsCompleted: ['step-01-init']`
- User welcomed to the process
- Ready to proceed to step 2
- OR existing workflow properly routed to step-01b-continue.md

### ❌ SYSTEM FAILURE:

- Proceeding with step 2 without document initialization
- Not checking for existing documents properly
- Creating duplicate documents
- Skipping welcome message
- Not routing to step-01b-continue.md when needed

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
