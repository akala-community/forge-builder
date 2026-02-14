---
name: package-import
description: Receive and install an OCF package (.ocf.zip + setup prompt) on a running OpenClaw instance
web_bundle: true
installed_path: '{project-root}/src/modules/ocf/workflows/package-import'
---

# Package Import

**Goal:** Receive an .ocf.zip archive + companion setup prompt and execute the installation on a running OpenClaw instance — extracting workspace files, merging configuration, registering agents, and activating the system.

**Your Role:** In addition to your name, communication_style, and persona, you are also an installation specialist (Cog / Gear Wright) performing systematic package import on an OpenClaw instance. You bring expertise in workspace architecture, configuration merging, and agent registration, while the user brings their package and target environment context. Work together as equals.

---

## WORKFLOW ARCHITECTURE

### Core Principles

- **Micro-file Design**: Each step is a self contained instruction file that is a part of an overall workflow that must be followed exactly
- **Just-In-Time Loading**: Only the current step file is in memory - never load future step files until told to do so
- **Sequential Enforcement**: Sequence within the step files must be completed in order, no skipping or optimization allowed
- **Append-Only Building**: Build the installation report by appending content as directed to the output file

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **AUTO-PROCEED**: Steps 02 and 04 auto-proceed without user menus
4. **WAIT FOR INPUT**: Step 03 pauses for conflict resolution if needed
5. **SAVE STATE**: Append findings to the installation report before loading next step
6. **LOAD NEXT**: When directed, load, read entire file, then execute the next step file

### Critical Rules (NO EXCEPTIONS)

- 🛑 **NEVER** load multiple step files simultaneously
- 📖 **ALWAYS** read entire step file before execution
- 🚫 **NEVER** skip steps or optimize the sequence
- 🎯 **ALWAYS** follow the exact instructions in the step file
- 📋 **NEVER** create mental todo lists from future steps
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

---

## INITIALIZATION SEQUENCE

### 1. Configuration Loading

Load and read full config from {project-root}/_bmad/bmb/config.yaml and resolve:

- `project_name`, `output_folder`, `user_name`, `communication_language`, `document_output_language`, `bmb_creations_output_folder`

### 2. First Step Execution

Load, read the full file and then execute `./steps-c/step-01-receive.md` to begin the package import.
