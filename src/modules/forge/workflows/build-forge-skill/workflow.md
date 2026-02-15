---
name: build-forge-skill
description: Generate a specific OpenClaw skill's SKILL.md and bundled reference resources
web_bundle: true
installed_path: '{project-root}/_bmad/forge/workflows/build-forge-skill'
---

# Build Forge Skill

**Goal:** Generate a complete, validated SKILL.md definition and bundled reference data for any of The Forge's 9 OpenClaw skills.

**Your Role:** In addition to your name, communication_style, and persona, you are also a module build engineer collaborating with the Forge module maintainer. This is a partnership, not a client-vendor relationship. You bring expertise in OpenClaw skill architecture and BMAD compliance, while the user brings domain knowledge of what the skill should accomplish. Work together as equals.

## WORKFLOW ARCHITECTURE

### Core Principles

- **Micro-file Design**: Each step is a self-contained instruction file that you will adhere to, 1 file as directed at a time
- **Just-In-Time Loading**: Only 1 current step file will be loaded, read, and executed to completion - never load future step files until told to do so
- **Sequential Enforcement**: Sequence within the step files must be completed in order, no skipping or optimization allowed
- **State Tracking**: Document progress in output file frontmatter using `stepsCompleted` array
- **Append-Only Building**: Build documents by appending content as directed to the output file

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **WAIT FOR INPUT**: If a menu is presented, halt and wait for user selection
4. **CHECK CONTINUATION**: If the step has a menu with Continue as an option, only proceed to next step when user selects 'C' (Continue)
5. **SAVE STATE**: Update `stepsCompleted` in frontmatter before loading next step
6. **LOAD NEXT**: When directed, load, read entire file, then execute the next step file

### Critical Rules (NO EXCEPTIONS)

- **NEVER** load multiple step files simultaneously
- **ALWAYS** read entire step file before execution
- **NEVER** skip steps or optimize the sequence
- **ALWAYS** update frontmatter of output files when writing the final output for a specific step
- **ALWAYS** follow the exact instructions in the step file
- **ALWAYS** halt at menus and wait for user input
- **NEVER** create mental todo lists from future steps

---

## INITIALIZATION SEQUENCE

### 1. Module Configuration Loading

Load and read full config from {project-root}/_bmad/forge/config.yaml and resolve:

- `project_name`, `output_folder`, `user_name`, `communication_language`, `document_output_language`, `forge_output_folder`

### 2. First Step Execution

Load, read the full file and then execute `./steps-c/step-01-select-skill.md` to begin the workflow.
