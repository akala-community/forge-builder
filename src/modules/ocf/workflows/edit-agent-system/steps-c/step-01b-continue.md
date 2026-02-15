---
name: 'step-01b-continue'
description: 'Handle workflow continuation from previous session'

outputFile: '{ocf_output_folder}/change-reports/change-report-{date}.md'
nextStepOptions:
  step-02: './step-02-identify-changes.md'
  step-03: './step-03-impact-analysis.md'
  step-04: './step-04-apply-changes.md'
  step-05: './step-05-coherence-check.md'
  step-06: './step-06-completion.md'
---

# Step 1b: Continue Workflow

## STEP GOAL:

To resume the edit-agent-system workflow from where it was left off in a previous session.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a workspace editor resuming a previous session
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response

### Step-Specific Rules:

- 🎯 Focus only on determining where to resume
- 🚫 FORBIDDEN to start new work -- just route to the correct step
- 💬 Present a clear summary of previous progress

## CONTEXT BOUNDARIES:

- User has run this workflow before
- Output file exists with stepsCompleted array
- Need to route to the correct next step

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly.

### 1. Welcome Back

"**Welcome back!** Let me check where we left off..."

### 2. Read stepsCompleted from Output

Load `{outputFile}` and read frontmatter:
- `stepsCompleted` array
- `lastStep` value
- `workspacePath` value

### 3. Present Progress Summary

"**Previous Session Summary:**

**Workspace:** {workspacePath}
**Steps Completed:** {list stepsCompleted}
**Last Step:** {lastStep}

**Progress:**
- [x] Step 01: Load Workspace {if in stepsCompleted}
- [{x or space}] Step 02: Identify Changes
- [{x or space}] Step 03: Impact Analysis
- [{x or space}] Step 04: Apply Changes
- [{x or space}] Step 05: Coherence Check
- [{x or space}] Step 06: Completion"

### 4. Determine Next Step

Find the last completed step and identify the next step to load from `{nextStepOptions}`.

"**Ready to resume from:** Step {N} - {step name}

[C] Continue from where we left off
[R] Restart from the beginning (will create new change report)"

### 5. Route to Correct Step

#### Menu Handling Logic:

- IF C: Load, read entire file, then execute the appropriate next step file from {nextStepOptions}
- IF R: Create new output file and load './step-01-init.md'
- IF Any other: help user respond, then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed when user makes a selection
- User can chat or ask questions -- always respond and then redisplay menu

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Previous output loaded and progress identified
- Clear summary presented to user
- Correct next step determined and loaded

### ❌ SYSTEM FAILURE:

- Not loading previous output file
- Routing to wrong step
- Starting new work instead of resuming

**Master Rule:** Read the existing output, determine where to resume, and route correctly.
