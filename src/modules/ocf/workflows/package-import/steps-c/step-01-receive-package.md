---
name: 'step-01-receive-package'
description: 'Get package path and target workspace, extract archive, read manifest, present summary for user confirmation'

nextStepFile: './step-02-validate-package.md'
packageStructureRef: '../data/package-structure-reference.md'
---

# Step 1: Receive Package

## STEP GOAL:

To get the `.ocf.zip` package path from the user, determine the target workspace directory, extract the archive to a temporary location, read the package manifest and setup prompt, present a summary, and get user confirmation before proceeding.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with 'C', ensure entire file is read
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are an installation specialist (Cog / Gear Wright)
- Systematic, precise, methodical
- You bring expertise in workspace architecture and package installation

### Step-Specific Rules:

- Focus ONLY on receiving the package, extracting, and presenting the summary
- FORBIDDEN to install any files to the target workspace yet - that comes in step 03
- FORBIDDEN to merge any configuration - that comes in step 04
- Ask for package path if not provided
- If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- Get package path and verify it exists
- Get target workspace path (or use default)
- Extract the archive to a temporary location
- Read manifest and setup prompt from the extracted package
- Present summary for user review
- DO NOT install or modify any target workspace files

## CONTEXT BOUNDARIES:

- User provides the .ocf.zip package path (or it may come from routing)
- This is the initialization step - gather inputs and present summary only
- No prior context needed
- Dependencies: none

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Get Package Path

**If package path was provided as an argument:**
- Use the provided path

**If no path was provided:**

"**Package Import**

I'll install an OpenClaw workspace package (`.ocf.zip`) into your workspace.

**Please provide the path to the `.ocf.zip` package file:**"

Wait for user to provide the path.

### 2. Verify Package Exists

Check that the provided path exists and is a `.ocf.zip` file. If it does not exist:

"**Error:** The path `{provided_path}` does not exist or is not a valid `.ocf.zip` file. Please provide a valid package path."

Wait for a corrected path.

### 3. Get Target Workspace Path

"**Where should this package be installed?**

1. **Default location:** `{ocf_output_folder}` (from your OCF configuration)
2. **Custom path:** Specify a different target directory

Enter a path, or press Enter / type 'default' to use the default location."

Wait for user input. If user provides a path, use it. If user enters nothing or 'default', use `{ocf_output_folder}`.

Verify the target directory exists or can be created.

### 4. Extract Archive

Extract the `.ocf.zip` file to a temporary working location (a subdirectory within the target path or a system temp folder).

"**Extracting package:** `{package_filename}`..."

List the top-level contents of the extracted archive. Record the full file listing for later validation.

### 5. Read Package Manifest

Look for the following metadata sources inside the extracted archive:

1. **Setup prompt** - A file matching the pattern `*.setup.md` at the root level of the archive
2. **AGENTS.md** - Check for OCF metadata in the YAML frontmatter (fields: `ocf_version`, `ocf_packaged`, `ocf_system_name`, `ocf_template_origins`)
3. **openclaw.json** - Configuration fragment, if present

Read and parse the setup prompt file. Extract the frontmatter metadata:
- `ocf_version`
- `system_name`
- `created` (package creation date)
- `template_origins`

If no setup prompt is found, check AGENTS.md frontmatter for OCF metadata. If neither is found, warn the user that the package may not be a standard OCF package, but allow them to proceed.

### 6. Build Package Summary

Compile a summary of the package contents:

**Workspace files found:**
- List each root file (AGENTS.md, SOUL.md, USER.md, IDENTITY.md, TOOLS.md, HEARTBEAT.md, MEMORY.md, BOOT.md, etc.)

**Directories found:**
- List directories (skills/, memory/, etc.) with file counts

**Configuration:**
- Note whether openclaw.json is present in the package

**OCF Metadata:**
- System name, OCF version, creation date, template origins

### 7. Present Summary and Confirm

"**Package Summary**

---

**Package:** `{package_filename}`
**System Name:** `{system_name}`
**OCF Version:** `{ocf_version}`
**Created:** `{creation_date}`

**Workspace Files:**
{list of workspace files found}

**Directories:**
{list of directories with file counts}

**Configuration:** {openclaw.json present/not present}
**Target:** `{target_workspace_path}`

---

**Ready to proceed with installation?**

**Select:** [C] Continue to validation"

#### Menu Handling Logic:

- IF C: Load, read entire file, then execute {nextStepFile}
- IF Any other: help user with questions or concerns, then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Package path obtained and verified as valid .ocf.zip
- Target workspace path determined
- Archive extracted to temporary location
- Setup prompt and/or OCF metadata read and parsed
- Package summary compiled with file listing
- User reviewed summary and confirmed
- Proceeding to validation

### FAILURE:

- Not verifying the package file exists
- Not extracting the archive before presenting summary
- Not reading the setup prompt or OCF metadata
- Installing files to the target workspace in this step
- Proceeding without user confirmation

**Master Rule:** This is the init step. Receive the package, extract it, read its manifest, present a summary. DO NOT install or modify any target files.
