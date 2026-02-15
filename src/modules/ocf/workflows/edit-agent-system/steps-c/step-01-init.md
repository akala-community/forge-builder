---
name: 'step-01-init'
description: 'Load existing workspace, inventory all artifacts, and initialize the change report'

nextStepFile: './step-02-identify-changes.md'
continueFile: './step-01b-continue.md'
outputFile: '{ocf_output_folder}/change-reports/change-report-{date}.md'
templateFile: '../templates/change-report-template.md'
artifactTypesData: '../data/artifact-types.csv'
---

# Step 1: Load Workspace

## STEP GOAL:

To load an existing OCF-generated workspace, inventory all artifacts present, validate the workspace structure, and initialize the change report document.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a workspace analyst and inventory specialist
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring OCF workspace architecture expertise, user brings their workspace and edit requirements

### Step-Specific Rules:

- 🎯 Focus only on loading, inventorying, and validating the workspace
- 🚫 FORBIDDEN to modify any workspace files in this step
- 🚫 FORBIDDEN to discuss what changes to make -- that's step 2
- 💬 Approach: Thorough inventory with clear reporting of what was found

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Create the change report from template and populate workspace summary
- 📖 Track progress in output frontmatter stepsCompleted
- 🚫 FORBIDDEN to proceed without a valid workspace loaded

## CONTEXT BOUNDARIES:

- This is the first step -- no prior context available
- User must provide a workspace path
- Focus: Loading and understanding what exists
- Dependencies: None

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Check for Existing Change Report (Continuation Detection)

Check if an output file already exists at `{outputFile}` (or scan `{ocf_output_folder}/change-reports/` for recent reports matching this workspace).

**IF existing report found with incomplete stepsCompleted:**
- "I found an existing change report from a previous session. Loading continuation..."
- Load, read entire file, then execute `{continueFile}`
- **STOP HERE** -- do not continue this step

**IF no existing report found:**
- Continue with this step

### 2. Get Workspace Path

"**Welcome to the Edit Agent System workflow.**

I'll help you modify an existing OpenClaw workspace while maintaining coherence across all artifacts.

**Please provide the path to the workspace you want to edit:**

This should be a directory containing OCF workspace artifacts (AGENTS.md, SOUL.md, skills/, etc.)"

Wait for user to provide the workspace path.

### 3. Validate Workspace Structure

Load and scan the provided workspace directory:

**Check for required files:**
- AGENTS.md (required)
- SOUL.md (required)

**Check for optional files:**
- USER.md
- MEMORY.md
- skills/ directory
- REVIEW.md
- openclaw.json
- tool-policies.md
- memory-config.md
- failover.md
- heartbeat.md
- logging.md
- orchestration.md

**IF AGENTS.md and SOUL.md are NOT found:**
"This doesn't appear to be a valid OCF workspace. I need at minimum AGENTS.md and SOUL.md.

Please check the path and try again."

Wait for corrected path. Loop until valid.

### 4. Inventory All Artifacts

Load `{artifactTypesData}` to understand artifact types and relationships.

For each artifact found in the workspace:
- Read the file completely
- Extract key metadata (agent name, role, capabilities)
- Note the file size and structure
- Identify cross-references to other artifacts

**For multi-agent workspaces:**
- Identify the agent roster (list all agents found)
- Map which artifacts belong to which agent
- Note the orchestration structure if present

### 5. Present Workspace Inventory

"**Workspace loaded successfully.**

**Path:** {workspace_path}
**Agents Found:** {count} ({list agent names})

**Artifact Inventory:**

| Artifact | Status | Agent | Size |
|----------|--------|-------|------|
| AGENTS.md | Found | {agent} | {lines} lines |
| SOUL.md | Found | {agent} | {lines} lines |
| USER.md | {Found/Missing} | {agent} | {lines} lines |
| MEMORY.md | {Found/Missing} | {agent} | {lines} lines |
| skills/ | {count} skills | {agent} | -- |
| REVIEW.md | {Found/Missing} | {agent} | {lines} lines |
| openclaw.json | {Found/Missing} | -- | {lines} lines |
| tool-policies.md | {Found/Missing} | {agent} | {lines} lines |
| ... | ... | ... | ... |

**Workspace Completeness:** {percentage}% of standard OCF artifacts present"

### 6. Initialize Change Report

Create `{outputFile}` from `{templateFile}`:

Set frontmatter values:
- `stepsCompleted: ['step-01-init']`
- `lastStep: 'step-01-init'`
- `date: {current date}`
- `user_name: {user_name}`
- `project_name: {project_name}`
- `workspacePath: {workspace_path}`

Append to the change report:

```markdown
## Workspace Summary

**Path:** {workspace_path}
**Date:** {date}
**Agents:** {agent list}

### Artifact Inventory

{full inventory table from step 5}

### Workspace Health

- **Completeness:** {percentage}%
- **Missing Standard Artifacts:** {list or "None"}
- **Agent Count:** {count}
```

### 7. Present Menu Options

Display: "**Workspace loaded and inventoried. Select an Option:** [C] Continue to Change Identification"

#### Menu Handling Logic:

- IF C: Save workspace summary to {outputFile}, update frontmatter stepsCompleted, then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#7-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- User can chat or ask questions -- always respond and then redisplay menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and the workspace summary is saved to the change report will you then load and read fully `{nextStepFile}` to execute change identification.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Workspace path obtained and validated
- All artifacts inventoried with counts
- Agent roster identified (for multi-agent workspaces)
- Change report initialized with workspace summary
- Frontmatter updated with stepsCompleted

### ❌ SYSTEM FAILURE:

- Proceeding without a valid workspace
- Not reading all artifact files
- Not identifying the agent roster
- Modifying any workspace files
- Discussing what changes to make (that's step 2)

**Master Rule:** Load and inventory EVERYTHING before proceeding. Do not modify anything. Do not discuss changes yet.
