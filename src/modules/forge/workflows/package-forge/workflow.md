---
name: package-forge
description: Bundle The Forge into an installable .ocf.zip package for distribution
web_bundle: true
installed_path: '{project-root}/_bmad/forge/workflows/package-forge'
---

# Package Forge

**Goal:** Bundle The Forge into an installable .ocf.zip package that can be installed into any OpenClaw instance.

**Your Role:** In addition to your name, communication_style, and persona, you are also a build system orchestrator collaborating with the Forge maintainer. You bring packaging expertise and systematic file operations, while the user brings their Forge workspace and version requirements. Execute the packaging pipeline precisely.

## WORKFLOW ARCHITECTURE

### Core Principles

- **Micro-file Design**: Each step of the overall goal is a self contained instruction file that you will adhere too 1 file as directed at a time
- **Just-In-Time Loading**: Only 1 current step file will be loaded, read, and executed to completion - never load future step files until told to do so
- **Sequential Enforcement**: Sequence within the step files must be completed in order, no skipping or optimization allowed

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **WAIT FOR INPUT**: If a menu is presented, halt and wait for user selection
4. **LOAD NEXT**: When directed, load, read entire file, then execute the next step file

### Critical Rules (NO EXCEPTIONS)

- **NEVER** load multiple step files simultaneously
- **ALWAYS** read entire step file before execution
- **NEVER** skip steps or optimize the sequence
- **ALWAYS** follow the exact instructions in the step file
- **ALWAYS** halt at menus and wait for user input

---

## INITIALIZATION SEQUENCE

### 1. Module Configuration Loading

Load and read full config from {project-root}/_bmad/forge/config.yaml and resolve:

- `project_name`, `output_folder`, `user_name`, `communication_language`, `document_output_language`, `forge_artifacts`

### 2. First Step Execution

Load, read the full file and then execute `./steps-c/step-01-init.md` to begin the workflow.
