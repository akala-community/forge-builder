---
name: 'step-01-load-workspace'
description: 'Get workspace path, inventory artifacts, initialize validation report'

nextStepFile: './step-02-structural-checks.md'
validationRules: '../data/workspace-validation-rules.md'
reportTemplate: '../templates/validation-report-template.md'
validationReportOutput: '{ocf_output_folder}/validation-report-{workspace_name}-{current_date}.md'
---

# Step 1: Load Workspace

## STEP GOAL:

To get the workspace path from the user, inventory all artifacts present in the workspace, and initialize the validation report.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a configuration validation specialist (Cog / Gear Wright)
- ✅ Systematic, thorough, objective
- ✅ You bring workspace architecture expertise

### Step-Specific Rules:

- 🎯 Focus ONLY on getting workspace path and inventorying artifacts
- 🚫 FORBIDDEN to run any validation checks yet — that comes in steps 02-04
- 💬 Ask for workspace path if not provided
- ⚙️ If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- 🎯 Get workspace path and verify it exists
- 💾 Create validation report from template
- 📖 Inventory all files and directories in workspace
- 🚫 DO NOT start checking file contents yet

## CONTEXT BOUNDARIES:

- User provides workspace path (or it may come from routing)
- This is the initialization step — gather inputs only
- No prior context needed
- Dependencies: none

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Get Workspace Path

**If workspace path was provided as an argument:**
- Use the provided path

**If no path was provided:**

"**Workspace Validation**

I'll check your OpenClaw workspace for internal consistency across all artifacts.

**Please provide the path to the workspace you want to validate:**

This should be the directory containing your agent's SOUL.md, AGENTS.md, and other workspace files."

Wait for user to provide the path.

### 2. Verify Workspace Exists

Check that the provided path exists and is a directory. If it doesn't exist:

"**Error:** The path `{provided_path}` does not exist or is not a directory. Please provide a valid workspace path."

### 3. Select Checks to Run

"**Which validation checks would you like to run?**

- **[A]ll** — Run all checks (structural, coherence, hardening) *(Recommended)*
- **[S]tructural** — File presence and well-formedness only
- **[C]oherence** — Cross-artifact consistency only
- **[H]ardening** — Security and resilience only"

Wait for selection. Default to All if user says yes/continue/proceed.

### 4. Inventory Workspace Artifacts

List ALL files and directories found in the workspace:

"**Inventorying workspace artifacts...**"

Use file I/O to list the workspace contents. Record:
- All `.md` files at root level
- All subdirectories (memory/, skills/, etc.)
- All files within subdirectories
- Whether openclaw.json exists (in workspace parent or project root)

### 5. Create Validation Report

Load {reportTemplate} and create the validation report at {validationReportOutput}.

Replace template placeholders:
- `{current_date}` → today's date
- `{workspace_path}` → the workspace path
- `{checks_run}` → which checks were selected

Replace the "## Workspace Inventory" section with the actual inventory:

```markdown
## Workspace Inventory

**Workspace Path:** {workspace_path}
**Files Found:** {count}

### Root Files
- {list each .md file with ✅ or ❌ status}

### Directories
- {list each directory and file count within}

### Configuration
- openclaw.json: {found/not found} at {path}
```

### 6. Present Inventory and Auto-Proceed

"**Workspace loaded and inventoried.**

**Path:** `{workspace_path}`
**Files found:** {count}
**Checks to run:** {selection}

**Proceeding to validation checks...**"

Save the report, then immediately load, read entire file, then execute {nextStepFile}.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Workspace path obtained and verified
- Check selection obtained
- All artifacts inventoried
- Validation report initialized
- Auto-proceeding to structural checks

### ❌ SYSTEM FAILURE:

- Not verifying workspace exists
- Starting validation checks before inventory
- Not creating the validation report
- Halting when should auto-proceed

**Master Rule:** This is the init step. Get inputs, inventory, initialize report, then auto-proceed. DO NOT start checking file contents.
