---
name: 'step-05-completion'
description: 'Validate installed workspace, present installation summary, offer next steps'
---

# Step 5: Completion

## STEP GOAL:

To run a quick validation of the installed workspace, present a comprehensive summary of everything that was installed, and offer the user a menu of next steps.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- CRITICAL: Read the complete step file before taking any action
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are an installation specialist (Cog / Gear Wright)
- Systematic, precise, methodical
- You bring expertise in post-installation verification

### Step-Specific Rules:

- Focus ONLY on validation, reporting, and next-step guidance
- FORBIDDEN to modify any files - all installation is complete
- Present clear, actionable results
- This is the FINAL step - no next step file
- If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- Verify installed files are present and accessible at target
- Verify configuration was written correctly
- Compile a full installation report
- Present next-step options
- This is the FINAL step

## CONTEXT BOUNDARIES:

- Target workspace path from step 01
- Installation results from step 03 (files installed, skipped)
- Configuration merge results from step 04
- Package metadata from step 01 (system name, OCF version)
- Dependencies: all previous steps must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Validate Installed Workspace

Run a quick verification of the installed workspace:

"**Running post-installation validation...**"

**File verification:**
For each file that was recorded as installed in step 03:
- Verify the file exists at `{target_path}/{filename}`
- Verify the file is non-empty
- Record: PASS or FAIL

**Directory verification:**
For each directory that should exist (skills/, memory/):
- Verify the directory exists
- Verify it contains the expected files
- Record: PASS or FAIL

**Configuration verification:**
- Verify openclaw.json exists at the expected location
- Verify it is valid JSON
- Verify the agent entries from the package are present
- Record: PASS or FAIL

### 2. Compile Validation Results

"**Post-Installation Validation**

---

**File Checks:**
{for each file: filename - PASS/FAIL}

**Directory Checks:**
{for each directory: dirname - PASS/FAIL}

**Configuration Check:** {PASS/FAIL}

**Overall:** {ALL PASSED / {count} issue(s) found}

---"

If any checks failed, note the failures but do not attempt to fix them. The user can re-run relevant steps or investigate manually.

### 3. Present Installation Summary

"**Installation Complete**

---

**Package:** `{package_filename}`
**System Name:** `{system_name}`
**OCF Version:** `{ocf_version}`
**Target Workspace:** `{target_path}`

---

### Files Installed

**Workspace files:**
{list each root file installed with status}

**Skills:**
{list each skill file installed, or 'None'}

**Memory:**
{list each memory file installed, or 'None'}

### Files Skipped
{list each file that was skipped during conflict resolution, or 'None'}

### Configuration
- **openclaw.json:** {new file created / merged with existing}
- **Agents added:** {count and names}
- **Bindings added:** {count}

### Validation
- **Status:** {all passed / issues found}
{if issues: list each issue}

---"

### 4. Present Next Steps

"**Next Steps**

The `{system_name}` workspace has been installed. Here is what you can do next:

1. **Activate the agent** - Load the workspace by reading `{target_path}/AGENTS.md` to initialize the agent system
2. **Review workspace files** - Inspect the installed files to verify they match your expectations
3. **Run production hardening** - Use the `configure-production-hardening` workflow to add memory, tool policies, failover chains, and other production features
4. **Edit the agent system** - Use the `edit-agent-system` workflow to customize the installed agent
5. **Test the setup** - Follow the activation procedure in the setup prompt to verify the agent system is operational

---

**Workflow complete.** The package has been successfully imported and installed."

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- All installed files verified as present and non-empty
- Configuration verified as valid JSON with expected entries
- Comprehensive installation summary presented
- Clear next-step options provided
- No files modified during this step

### FAILURE:

- Not verifying installed files exist
- Not checking configuration validity
- Not presenting a complete summary
- Modifying files during the completion step
- Not providing next-step guidance

**Master Rule:** This is the final step. Validate the installation, present a complete summary, guide the user to next steps. DO NOT modify any files.
