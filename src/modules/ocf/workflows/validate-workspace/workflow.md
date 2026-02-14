---
name: validate-workspace
description: Validate OpenClaw workspace for structural integrity, cross-artifact coherence, and production hardening
web_bundle: true
installed_path: '{project-root}/src/modules/ocf/workflows/validate-workspace'
---

# Validate Workspace

**Goal:** Check a generated OpenClaw workspace for structural integrity, cross-artifact coherence, and production hardening — verifying that required files exist, personalities match directives, skills are present, bindings are complete, hardening is configured, and all cross-references resolve.

**Your Role:** In addition to your name, communication_style, and persona, you are also a configuration validation specialist (Cog / Gear Wright) performing systematic quality assurance on OpenClaw agent workspaces. You bring expertise in workspace architecture standards, while the workspace artifacts provide the data to validate. Your job is to be thorough, objective, and systematic.

---

## WORKFLOW ARCHITECTURE

### Core Principles

- **Micro-file Design**: Each step is a self contained instruction file that is a part of an overall workflow that must be followed exactly
- **Just-In-Time Loading**: Only the current step file is in memory - never load future step files until told to do so
- **Sequential Enforcement**: Sequence within the step files must be completed in order, no skipping or optimization allowed
- **Append-Only Building**: Build the validation report by appending content as directed to the output file

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **AUTO-PROCEED**: Validation steps 02-04 auto-proceed without user menus
4. **SAVE STATE**: Append findings to the validation report before loading next step
5. **LOAD NEXT**: When directed, load, read entire file, then execute the next step file

### Critical Rules (NO EXCEPTIONS)

- NEVER load multiple step files simultaneously
- ALWAYS read entire step file before execution
- NEVER skip steps or optimize the sequence
- ALWAYS follow the exact instructions in the step file
- NEVER create mental todo lists from future steps
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

---

## INITIALIZATION SEQUENCE

### 1. Configuration Loading

Load and read full config from {project-root}/_bmad/ocf/config.yaml and resolve:

- `project_name`, `output_folder`, `user_name`, `communication_language`, `document_output_language`, `ocf_output_folder`

### 2. First Step Execution

Load, read the full file and then execute `./steps-c/step-01-load-workspace.md` to begin the workspace validation.
