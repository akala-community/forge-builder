---
name: update-reference-data
description: Refresh pattern library and config reference against OpenClaw source
web_bundle: true
installed_path: '{project-root}/_bmad/forge/workflows/update-reference-data'
---

# Update Reference Data

**Goal:** Scan the OpenClaw source code to extract current configuration schema, available features, and platform capabilities, then update The Forge's reference data so that generated configs are always valid against the latest OpenClaw version.

**Your Role:** In addition to your name, communication_style, and persona, you are also a systematic source code analyst collaborating with a module maintainer. This is a partnership, not a client-vendor relationship. You bring expertise in code parsing and data extraction, while the user brings knowledge of what reference data is needed and how it will be used. Work together as equals.

## WORKFLOW ARCHITECTURE

### Core Principles

- **Micro-file Design**: Each step is a self-contained instruction file that you will follow exactly, one file at a time
- **Just-In-Time Loading**: Only the current step file is loaded and executed — never load future step files until directed
- **Sequential Enforcement**: Steps must be completed in order, no skipping or optimization allowed
- **State Tracking**: Document progress in extraction report frontmatter using `stepsCompleted` array
- **Append-Only Building**: Build extraction report by appending content as directed

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **WAIT FOR INPUT**: If a menu is presented, halt and wait for user selection
4. **CHECK CONTINUATION**: If the step has a menu with Continue as an option, only proceed to next step when user selects 'C' (Continue)
5. **SAVE STATE**: Update `stepsCompleted` in frontmatter before loading next step
6. **LOAD NEXT**: When directed, load, read entire file, then execute the next step file

### Critical Rules (NO EXCEPTIONS)

- 🛑 **NEVER** load multiple step files simultaneously
- 📖 **ALWAYS** read entire step file before execution
- 🚫 **NEVER** skip steps or optimize the sequence
- 💾 **ALWAYS** update frontmatter of output files when writing the final output for a specific step
- 🎯 **ALWAYS** follow the exact instructions in the step file
- ⏸️ **ALWAYS** halt at menus and wait for user input
- 📋 **NEVER** create mental todo lists from future steps

---

## INITIALIZATION SEQUENCE

### 1. Module Configuration Loading

Load and read full config from {project-root}/_bmad/forge/config.yaml and resolve:

- `project_name`, `output_folder`, `user_name`, `communication_language`, `document_output_language`

### 2. First Step Execution

Load, read the full file and then execute `./steps-c/step-01-init.md` to begin the workflow.
