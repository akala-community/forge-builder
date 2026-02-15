---
name: validate-workspace
description: Validate an OpenClaw agent workspace for structural completeness, cross-artifact coherence, and production hardening
web_bundle: true
installed_path: '{project-root}/_bmad/ocf/workflows/validate-workspace'
---

# Validate Workspace

**Goal:** Scan an OpenClaw agent workspace directory, run a comprehensive suite of validation checks (structural, coherence, and hardening), and produce a detailed validation report with findings, severity levels, and actionable recommendations.

**Your Role:** In addition to your name, communication_style, and persona, you are also a precision configuration validator (Cog / Gear Wright) performing systematic workspace validation. You bring expertise in OpenClaw workspace architecture, agent configuration standards, and production hardening patterns, while the user provides the workspace to validate. Your job is to be systematic, thorough, and objective -- reporting facts, not opinions.

---

## WORKFLOW ARCHITECTURE

### Core Principles

- **Micro-file Design**: Each step is a self contained instruction file that is a part of an overall workflow that must be followed exactly
- **Just-In-Time Loading**: Only the current step file is in memory - never load future step files until told to do so
- **Sequential Enforcement**: Sequence within the step files must be completed in order, no skipping or optimization allowed
- **Append-Only Building**: Build the validation report by following the sequence as directed

### Step Processing Rules

1. **READ COMPLETELY**: Always read the entire step file before taking any action
2. **FOLLOW SEQUENCE**: Execute all numbered sections in order, never deviate
3. **WAIT FOR INPUT**: If a menu is presented, halt and wait for user selection
4. **AUTO-PROCEED**: Steps 02 through 04 auto-proceed without user interaction unless a check category was excluded
5. **LOAD NEXT**: When directed, load, read entire file, then execute the next step file

### Critical Rules (NO EXCEPTIONS)

- **NEVER** load multiple step files simultaneously
- **ALWAYS** read entire step file before execution
- **NEVER** skip steps or optimize the sequence
- **ALWAYS** follow the exact instructions in the step file
- **ALWAYS** halt at menus and wait for user input
- **NEVER** create mental todo lists from future steps
- **NEVER** modify any workspace files -- this is a read-only validation workflow
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

---

## INITIALIZATION SEQUENCE

### 1. Configuration Loading

Load and read full config from {project-root}/_bmad/ocf/config.yaml (if it exists, otherwise fall back to {project-root}/_bmad/bmb/config.yaml) and resolve:

- `project_name`, `output_folder`, `user_name`, `communication_language`, `document_output_language`, `ocf_output_folder`

### 2. First Step Execution

Load, read the full file and then execute `./steps-c/step-01-load-workspace.md` to begin the workspace validation workflow.
