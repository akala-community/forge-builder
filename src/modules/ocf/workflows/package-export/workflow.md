---
name: package-export
description: Bundle workspace into portable zip + setup prompt
web_bundle: true
installed_path: '{project-root}/_bmad/ocf/workflows/package-export'
---

# Package Export

**Goal:** Bundle a completed OpenClaw workspace into a portable `.ocf.zip` archive with a companion `setup.md` prompt that guides a receiving agent through unpacking and activating the system.

**Your Role:** In addition to your name, communication_style, and persona, you are also an assembly and packaging specialist (Cog / Gear Wright) performing systematic workspace bundling. You bring expertise in workspace architecture, metadata injection, and portable packaging, while the user provides the completed workspace to export. Your job is to be precise, methodical, and thorough.

---

## WORKFLOW ARCHITECTURE

### Core Principles

- **Micro-file Design**: Each step is a self contained instruction file that is a part of an overall workflow that must be followed exactly
- **Just-In-Time Loading**: Only the current step file is in memory - never load future step files until told to do so
- **Sequential Enforcement**: Sequence within the step files must be completed in order, no skipping or optimization allowed
- **Append-Only Building**: Build the setup.md document by following template structure as directed

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **WAIT FOR INPUT**: If a menu is presented, halt and wait for user selection
4. **CHECK CONTINUATION**: If the step has a menu with Continue as an option, only proceed to next step when user selects 'C' (Continue)
5. **LOAD NEXT**: When directed, load, read entire file, then execute the next step file

### Critical Rules (NO EXCEPTIONS)

- 🛑 **NEVER** load multiple step files simultaneously
- 📖 **ALWAYS** read entire step file before execution
- 🚫 **NEVER** skip steps or optimize the sequence
- 🎯 **ALWAYS** follow the exact instructions in the step file
- ⏸️ **ALWAYS** halt at menus and wait for user input
- 📋 **NEVER** create mental todo lists from future steps
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

---

## INITIALIZATION SEQUENCE

### 1. Configuration Loading

Load and read full config from {project-root}/_bmad/bmb/config.yaml and resolve:

- `project_name`, `output_folder`, `user_name`, `communication_language`, `document_output_language`, `bmb_creations_output_folder`

Also load OCF module config from {project-root}/src/modules/ocf/module.yaml and resolve:

- `ocf_output_folder`

### 2. First Step Execution

Load, read the full file and then execute `./steps-c/step-01-load-workspace.md` to begin the package export workflow.
