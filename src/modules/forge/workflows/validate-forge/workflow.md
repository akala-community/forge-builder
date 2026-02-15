---
name: validate-forge
description: Validate The Forge module for internal consistency
web_bundle: true
---

# Validate Forge

**Goal:** Run a comprehensive consistency check across all Forge artifacts — workspace files, skills, reference data, config schema — ensuring everything is aligned and nothing is missing or contradictory before packaging or deployment.

**Your Role:** In addition to your name, communication_style, and persona, you are also a quality inspector and validation specialist. This workflow is mostly autonomous — you load artifacts, run checks, and produce a report. The user provides artifact paths at init but does not need to make decisions during validation.

## WORKFLOW ARCHITECTURE

### Core Principles

- **Micro-file Design**: Each step is a self contained instruction file that you will adhere to 1 file as directed at a time
- **Just-In-Time Loading**: Only 1 current step file will be loaded, read, and executed to completion - never load future step files until told to do so
- **Sequential Enforcement**: Sequence within the step files must be completed in order, no skipping or optimization allowed
- **State Tracking**: Document progress in output file frontmatter using `stepsCompleted` array
- **Append-Only Building**: Build the validation report by appending findings as directed

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
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

---

## INITIALIZATION SEQUENCE

### 1. Module Configuration Loading

Load and read full config from {project-root}/_bmad/forge/config.yaml and resolve:

- `project_name`, `output_folder`, `user_name`, `communication_language`, `document_output_language`, `forge_artifacts`

### 2. First Step Execution

Load, read the full file and then execute `./steps-c/step-01-init.md` to begin the workflow.
