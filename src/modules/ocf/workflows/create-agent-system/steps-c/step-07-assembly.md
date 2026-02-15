---
name: 'step-07-assembly'
description: 'Read workspace-plan.md and assemble the complete workspace directory structure by writing all artifact files to disk'

nextStepFile: './step-08-review.md'
outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'
directoryStructure: '../data/workspace-directory-structure.md'
assemblyTemplates: '../data/assembly-templates.md'
---

# Step 7: Assembly

## STEP GOAL:

To read workspace-plan.md completely, extract all generated artifact content, and assemble the complete workspace directory structure by writing every individual artifact file to disk. This is the Cog (Gear Wright) phase — precision assembly of all parts into a functioning workspace.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Cog (Gear Wright) — assembly and structure expert for OpenClaw workspaces
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ You specialize in precise file assembly, directory construction, and artifact placement
- ✅ Every file must land in the correct location with the correct content — no approximations

### Step-Specific Rules:

- 🎯 Focus ONLY on assembling files from workspace-plan.md content to disk — do NOT generate new content
- 🚫 FORBIDDEN to modify, improve, or alter any artifact content during assembly — write exactly what was generated in prior steps
- 🚫 FORBIDDEN to skip any agent or any artifact in the roster
- 📋 Follow the directory structure standard from {directoryStructure} strictly
- 💾 This step is purely mechanical — read content from workspace-plan.md, write to correct file paths

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Write all artifact files using file I/O to the correct workspace paths
- 📖 Update stepsCompleted and Generation Progress table in {outputFile} frontmatter when done
- 🚫 FORBIDDEN to proceed without all files written and verified
- 📋 Build a complete file manifest tracking every file written with its full path

## CONTEXT BOUNDARIES:

- Available: workspace-plan.md with all generated artifact content from steps 02-06
- Focus: Assembly — reading content and writing files to disk
- Limits: Do NOT generate, modify, or enhance any content — assemble only
- Dependencies: Requires completed steps 01 through 06 with all artifact content present in workspace-plan.md

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Workspace Plan Completely

Load {outputFile} (workspace-plan.md) entirely. Extract:
- `system_name` from frontmatter
- Agent roster (all agent names in kebab-case)
- ALL generated artifact content for each agent (SOUL.md, IDENTITY.md, AGENTS.md (with self-correction directives integrated), USER.md, MEMORY.md, TOOLS.md, HEARTBEAT.md, BOOT.md, SKILL.md per skill)
- ALL per-agent openclaw.json config content

**If any required content is missing from workspace-plan.md:**

"**Warning:** The following artifacts are missing from workspace-plan.md:
{list missing artifacts with the step that should have generated them}

Assembly cannot proceed with missing artifacts. Please go back to the appropriate step to generate the missing content.

**Missing from:** {step name(s)}"

HALT — do not proceed with partial assembly.

### 2. Load Reference Files

Load {directoryStructure} for the canonical workspace directory layout.
Load {assemblyTemplates} for the file manifest and assembly summary templates.

### 3. Generate Supporting Files

Before assembling, generate the following supporting files that were not created in prior steps. These complete the workspace:

a. **TOOLS.md** — Local tool and environment notes for each agent. Create with sections relevant to this agent's skills. Reference the agent's skill artifacts for relevant tool documentation.

b. **HEARTBEAT.md** — Periodic task checklist for each agent. If the agent uses heartbeats (per config), populate with initial check tasks. Otherwise create with empty task list.

c. **BOOT.md** — Boot sequence for each agent. Define session startup behavior and context loading sequence.

d. **MEMORY.md** — Free-form long-term memory document for each agent. This is intentionally unstructured — the agent fills it in over time. Start mostly empty with a brief header.

Append all generated supporting files to {outputFile} under each agent's section.

### 4. Create Directory Structure

Create all required directories using file I/O. Create one `agents/{agent-name}/` directory (with `skills/` and `memory/` subdirectories) for EACH agent in the roster. Confirm all directories are created before proceeding to file writes.

### 5. Write Agent Artifact Files

**DO NOT BE LAZY — For EACH agent in the roster, write ALL artifact files:**

For each agent `{agent-name}`, write to disk:
- `agents/{agent-name}/SOUL.md` — extract SOUL.md content from workspace-plan.md
- `agents/{agent-name}/IDENTITY.md` — extract IDENTITY.md content
- `agents/{agent-name}/AGENTS.md` — extract AGENTS.md content (with self-correction directives integrated)
- `agents/{agent-name}/USER.md` — extract USER.md content
- `agents/{agent-name}/MEMORY.md` — extract MEMORY.md content (free-form)
- `agents/{agent-name}/TOOLS.md` — extract TOOLS.md content
- `agents/{agent-name}/HEARTBEAT.md` — extract HEARTBEAT.md content
- `agents/{agent-name}/BOOT.md` — extract BOOT.md content
- `agents/{agent-name}/skills/{skill-name}/SKILL.md` — for EACH skill, extract SKILL.md content

All paths are relative to `{ocf_output_folder}/{system_name}/`. Track every file written with its full path in a running file manifest.

### 6. Write Per-Agent Config

For each agent, write their openclaw.json to `{ocf_output_folder}/{system_name}/agents/{agent-name}/openclaw.json`.

### 7. Update Workspace Plan with File Manifest and Assembly Status

Update {outputFile} frontmatter:
- Add `stepsCompleted` entry: 'step-07-assembly'
- Update `lastStep`: 'step-07-assembly'
- Update Generation Progress table: mark step 07 as complete

Append a **File Manifest** section to {outputFile} using the template from {assemblyTemplates}. Fill in all actual file paths and counts.

### 8. Present Assembly Summary

Present the assembly summary using the template from {assemblyTemplates}. Fill in actual system name, workspace location, directory tree (showing all agents and their files), and accurate file/directory/agent/skill counts.

### 9. Present MENU OPTIONS

Display: **Select:** [C] Continue to Review

#### Menu Handling Logic:

- IF C: Save file manifest and assembly status to {outputFile}, update frontmatter stepsCompleted to include 'step-07-assembly', update Generation Progress table (mark step 07 as complete), then load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then [Redisplay Menu Options](#9-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and ALL artifact files have been written to disk with the file manifest appended to {outputFile} will you then load and read fully `{nextStepFile}` to execute the review step.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- workspace-plan.md loaded completely with all artifact content
- Directory structure standard loaded from {directoryStructure}
- All directories created (agents/{name}/, agents/{name}/skills/, agents/{name}/memory/)
- SOUL.md, IDENTITY.md, AGENTS.md, USER.md, MEMORY.md, TOOLS.md, HEARTBEAT.md, BOOT.md written for EVERY agent
- SKILL.md files written for every skill of every agent
- Per-agent openclaw.json written
- File manifest appended to workspace-plan.md with all paths and statuses
- stepsCompleted updated in frontmatter
- Assembly summary presented with accurate file and directory counts

### SYSTEM FAILURE:

- Skipping any agent or any artifact file
- Modifying, improving, or generating new content during assembly
- Not creating all required directories before writing files
- Not building the per-agent openclaw.json
- Missing any config or workspace file
- Not appending file manifest to workspace-plan.md
- Inaccurate file counts in the summary
- Proceeding with partial assembly when artifacts are missing

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE. Every file in every agent directory must be written. No exceptions.
