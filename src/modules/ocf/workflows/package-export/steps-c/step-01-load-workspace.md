---
name: 'step-01-load-workspace'
description: 'Get workspace path, validate completeness, extract system name and packaging parameters'

nextStepFile: './step-02-metadata-injection.md'
---

# Step 1: Load Workspace

## STEP GOAL:

To get the workspace path from the user, validate that it contains the required artifacts for a complete workspace, extract the system name, and gather optional packaging parameters.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are an assembly and packaging specialist (Cog / Gear Wright)
- ✅ Systematic, precise, methodical
- ✅ You bring workspace architecture and packaging expertise

### Step-Specific Rules:

- 🎯 Focus ONLY on loading workspace, validating completeness, and extracting system name
- 🚫 FORBIDDEN to modify any workspace files yet — that comes in step 02
- 🚫 FORBIDDEN to generate setup.md yet — that comes in step 03
- 💬 Ask for workspace path if not provided
- ⚙️ If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- 🎯 Get workspace path and verify it exists
- 💾 Inventory all workspace artifacts
- 📖 Extract system name from workspace
- 🚫 DO NOT modify any workspace files

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

"**Package Export**

I'll bundle your completed OpenClaw workspace into a portable `.ocf.zip` archive with a companion setup prompt.

**Please provide the path to the workspace you want to package:**

This should be the directory containing your agent's SOUL.md, AGENTS.md, and other workspace files."

Wait for user to provide the path.

### 2. Verify Workspace Exists

Check that the provided path exists and is a directory. If it doesn't exist:

"**Error:** The path `{provided_path}` does not exist or is not a directory. Please provide a valid workspace path."

### 3. Validate Workspace Completeness

Inventory the workspace and check for required artifacts:

"**Validating workspace completeness...**"

**Required files (must exist):**
- AGENTS.md
- SOUL.md
- USER.md

**Expected files (warn if missing):**
- openclaw.json (in workspace or parent project)
- MEMORY.md
- IDENTITY.md
- TOOLS.md

**Expected directories (warn if missing):**
- skills/
- memory/

List all files found. For each required file that is missing, report an error. For each expected file that is missing, report a warning.

**If any REQUIRED files are missing:**

"**Error:** Your workspace is missing required files: {list missing}

A workspace must contain at minimum: AGENTS.md, SOUL.md, USER.md.

Please complete your workspace before packaging, or run the validate-workspace workflow first.

Would you like to proceed anyway? [Y/N]"

If N, halt the workflow.
If Y, note the incomplete status and continue.

### 4. Extract System Name

Determine the system name for the package:

1. Check if openclaw.json exists and contains a system name or project name
2. If not, derive from the workspace folder name
3. Present the extracted name to the user

"**System name detected:** `{system_name}`

This will be used for:
- `{system_name}.ocf.zip` — the archive file
- `{system_name}.setup.md` — the setup prompt

Is this correct, or would you like to use a different name?"

Wait for confirmation or alternative name.

### 5. Gather Optional Parameters

"**Optional packaging parameters:**

1. **Custom setup instructions** — Any additional instructions to include in the setup prompt? (Enter text or skip)
2. **Target OCF version** — Specific OCF version to stamp? (Enter version or skip for current)

Enter your responses, or type 'skip' to use defaults."

Record any custom instructions and target version.

### 6. Present Summary and Continue

"**Workspace loaded and validated.**

**Path:** `{workspace_path}`
**System Name:** `{system_name}`
**Files found:** {count}
**Status:** {complete/incomplete with warnings}
**Custom Instructions:** {yes/no}
**OCF Version:** {version or 'current'}

**Select:** [C] Continue to metadata injection"

#### Menu Handling Logic:

- IF C: Load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Workspace path obtained and verified
- Workspace artifacts inventoried
- Required files validated (or user acknowledged gaps)
- System name extracted and confirmed
- Optional parameters gathered
- Proceeding to metadata injection

### ❌ SYSTEM FAILURE:

- Not verifying workspace exists
- Not checking for required files
- Starting to modify files before step 02
- Not confirming system name with user
- Proceeding without user confirmation

**Master Rule:** This is the init step. Get inputs, validate completeness, extract system name, gather parameters. DO NOT modify any files.
