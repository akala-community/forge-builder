---
name: 'step-01b-continue'
description: 'Handle workflow continuation from previous session'

outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'
---

# Step 1b: Continue Workflow

## STEP GOAL:

To resume the create-agent-system workflow from where it was left off in a previous session by reading the workspace plan, identifying the last completed step, and routing to the next step.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are an OpenClaw workspace generator resuming a previous session
- ✅ We engage in collaborative dialogue, not command-response

### Step-Specific Rules:

- 🎯 Focus only on reading progress and routing to the correct next step
- 🚫 FORBIDDEN to regenerate content that has already been completed
- 💬 Present clear progress summary before continuing

## EXECUTION PROTOCOLS:

- 🎯 Load workspace-plan.md and read stepsCompleted
- 💾 Do NOT modify workspace-plan.md in this step
- 📖 Route to the correct next step based on progress
- 🚫 FORBIDDEN to skip steps or jump ahead

## CONTEXT BOUNDARIES:

- User has run this workflow before
- workspace-plan.md exists with stepsCompleted array
- Need to determine and route to the correct next step

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Welcome Back

"**Welcome back!** Let me check where we left off with your agent system workspace..."

### 2. Read Progress from Workspace Plan

Load {outputFile} and read frontmatter:
- `stepsCompleted` array
- `lastStep` value
- `system_name`
- `agent_count`

### 3. Present Progress Summary

"**Workspace:** {system_name}
**Agents:** {agent_count}
**Last completed step:** {lastStep}

**Progress:**
{Display the Generation Progress table from workspace-plan.md with current status}"

### 4. Determine Next Step

Map the last completed step to the next step file:

| Last Completed | Next Step File |
|---------------|----------------|
| step-01-init | ./step-02-identity.md |
| step-02-identity | ./step-03-context.md |
| step-03-context | ./step-04-skills.md |
| step-04-skills | ./step-05-config.md |
| step-05-config | ./step-06-self-correction.md |
| step-06-self-correction | ./step-07-assembly.md |
| step-07-assembly | ./step-08-review.md |

### 5. Route to Next Step

"**Ready to continue with: {next step name}**

Loading next step..."

Update `lastContinued` date in {outputFile} frontmatter, then load, read entirely, and execute the determined next step file.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Workspace plan loaded and progress read correctly
- Clear progress summary presented to user
- Correct next step identified and loaded
- lastContinued date updated

### ❌ SYSTEM FAILURE:

- Not reading stepsCompleted array
- Routing to wrong step
- Regenerating already-completed content
- Not presenting progress summary

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
