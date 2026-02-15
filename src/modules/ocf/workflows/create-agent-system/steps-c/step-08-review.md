---
name: 'step-08-review'
description: 'Present the complete generated workspace for user review and refinement — FINAL STEP'

outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'
reviewTemplates: '../data/review-templates.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'
---

# Step 8: Review (Final Step)

## STEP GOAL:

To present the complete generated workspace for interactive user review and refinement. The user can inspect any agent, edit any artifact, run advanced elicitation or party mode for quality review, and ultimately mark the workspace as complete. This is the final step of the create-agent-system workflow.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are a collaborative reviewer — facilitating workspace quality review
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ The user has final authority over workspace completeness — never mark complete without explicit user confirmation

### Step-Specific Rules:

- 🎯 Focus on presenting, reviewing, and refining the assembled workspace
- 🚫 FORBIDDEN to mark the workspace as complete without explicit user confirmation via 'D' selection
- 🚫 FORBIDDEN to skip presenting the workspace overview
- 💬 This is an interactive review loop — the user drives what gets reviewed and edited
- 📋 All edits must be written back to disk immediately after user confirms changes
- 🚪 This is the FINAL step — there is no next step file

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Load workspace-plan.md and read the file manifest to know all file locations
- 📖 Present workspace overview before offering review menu
- 🚫 FORBIDDEN to auto-complete — user must explicitly select 'D' to finish
- 📋 After any edit, write changes to disk and update the file on the filesystem

## CONTEXT BOUNDARIES:

- Available: workspace-plan.md with file manifest, all assembled artifact files on disk
- Focus: Review, inspection, and refinement of the complete workspace
- Limits: Do NOT generate entirely new agents or restructure the workspace — only review and edit existing artifacts
- Dependencies: Requires completed step-07 with all files assembled to disk
- Finality: This is the last step — completion ends the workflow

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Workspace Plan and File Manifest

Load {outputFile} (workspace-plan.md) completely. Extract system_name, agent roster, file manifest, and Generation Progress table.

Verify that step-07-assembly is in `stepsCompleted`. If not:

"**Error:** Assembly step has not been completed. The workspace must be assembled before review. Please return to step 07 to assemble the workspace first."

HALT — do not proceed without completed assembly.

### 2. Present Workspace Overview

Load {reviewTemplates} and use the **Workspace Overview Template** to present the workspace summary. Fill in actual system name, workspace location, agent count, file count, agent table with artifact and skill counts, and config file statuses.

### 3. Present MENU OPTIONS

Display: **Select an Option:** [R] Review Agent [E] Edit Artifact [A] Advanced Elicitation [P] Party Mode [D] Done

#### Menu Handling Logic:

- **IF R (Review Agent):**
  Ask which agent to review (numbered list). Load and present ALL artifacts for that agent from disk (SOUL.md, IDENTITY.md, AGENTS.md, USER.md, MEMORY.md, TOOLS.md, HEARTBEAT.md, BOOT.md, all skill files, openclaw.json). After presenting: "**Review of {agent-display-name} complete. Any changes needed? Select [E] to edit, or choose another option.**"
  [Redisplay Menu Options](#3-present-menu-options)

- **IF E (Edit Artifact):**
  Ask which file to edit (path or agent-name + artifact). Load current content from disk and present. Ask what changes to make. Apply modifications and present updated content for confirmation: **Save?** [Y] Yes [N] No.
  - IF Y: Write to disk. "**Changes saved.**"
  - IF N: "**Changes discarded.**"
  [Redisplay Menu Options](#3-present-menu-options)

- **IF A (Advanced Elicitation):**
  Execute {advancedElicitationTask} for structured quality review. Present findings.
  [Redisplay Menu Options](#3-present-menu-options)

- **IF P (Party Mode):**
  Execute {partyModeWorkflow} for multi-perspective review. Present findings.
  [Redisplay Menu Options](#3-present-menu-options)

- **IF D (Done):**
  Confirm: "**Are you sure you want to mark this workspace as complete?** System: {system_name}, Agents: {count}, Files: {count}. Once marked complete, the workflow will end. [Y] Yes [N] No"
  - IF N: [Redisplay Menu Options](#3-present-menu-options)
  - IF Y: Proceed to [Finalize Workspace](#4-finalize-workspace)

- **IF Any other:** Help user understand options, then [Redisplay Menu Options](#3-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY mark workspace as complete when user selects 'D' AND confirms with 'Y'
- After R, E, A, or P actions, ALWAYS return to the menu
- All edits via 'E' must be written to disk immediately after user confirms
- Never auto-complete or assume the user is done

### 4. Finalize Workspace

Update {outputFile} frontmatter:
- Add `stepsCompleted` entry: 'step-08-review'
- Update `lastStep`: 'step-08-review'
- Add `status`: 'COMPLETE'
- Add `completionDate`: '{current_date}'

Update Generation Progress table: mark step 08 as complete.

### 5. Present Final Summary

Load {reviewTemplates} and use the **Final Summary Template** to present the completion message. Fill in actual system name, workspace location, completion date, agent table with roles and counts, total file count, and workspace directory tree.

## CRITICAL STEP COMPLETION NOTE

This is the FINAL step. There is no next step file. Once the user selects 'D' and confirms, the workspace is marked COMPLETE and the workflow ends. Do NOT attempt to load any further steps.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- workspace-plan.md loaded with file manifest from step 07
- Workspace overview presented with accurate counts
- Interactive review menu presented with all options (R, E, A, P, D)
- Review (R) loads artifacts from disk, not workspace-plan.md
- Edit (E) loads file, accepts modifications, confirms, writes to disk
- Done (D) requires explicit user confirmation before marking complete
- workspace-plan.md updated with status: COMPLETE and completionDate
- Final summary presented with complete workspace overview
- Workflow ends cleanly after final summary

### SYSTEM FAILURE:

- Not presenting workspace overview before the review menu
- Not loading artifact files from disk when reviewing
- Not writing edits to disk after user confirms
- Marking complete without explicit 'D' then 'Y' confirmation
- Attempting to load a next step (there is none)
- Not returning to menu after R, E, A, or P actions

**Master Rule:** The user must explicitly confirm completion. No auto-completing. No exceptions.
