---
name: 'step-04-package-assembly'
description: 'Bundle workspace files and setup.md into portable .ocf.zip archive'
ocfOutputFolder: '{ocfOutputFolder}'
---

# Step 4: Package Assembly

## STEP GOAL:

To bundle all workspace files and the generated setup.md into a portable `{system_name}.ocf.zip` archive, verify its contents, and present the final output paths to the user.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are an assembly and packaging specialist (Cog / Gear Wright)
- ✅ Systematic, precise, methodical
- ✅ You bring expertise in archive creation and portable packaging

### Step-Specific Rules:

- 🎯 Focus ONLY on creating the zip archive and verifying its contents
- 💬 Report final output paths clearly
- ⚙️ If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- 🎯 Create the .ocf.zip archive
- 💾 Verify archive contents
- 📖 Present final summary
- This is the FINAL step — no next step

## CONTEXT BOUNDARIES:

- Workspace path, system name from step 01
- Modified workspace artifacts from step 02
- Setup.md from step 03 at `{ocfOutputFolder}/packages/{system_name}.setup.md`
- Dependencies: steps 01, 02, and 03 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Prepare Package Directory

Ensure the output directory exists:
`{ocfOutputFolder}/packages/`

Create it if it doesn't exist.

### 2. Create ZIP Archive

Create a zip archive at:
`{ocfOutputFolder}/packages/{system_name}.ocf.zip`

**Contents to include:**
- All files from the workspace directory (maintaining relative directory structure)
- The setup.md file (place at root level of archive as `{system_name}.setup.md`)

**Zip creation approach:**
Use the file I/O tools available to create the archive. The archive should:
- Use relative paths (no absolute paths inside the archive)
- Maintain the workspace directory structure
- Include the setup.md at the archive root level

"**Creating archive:** `{system_name}.ocf.zip`..."

### 3. Verify Archive Contents

After creating the archive, verify:

1. The archive file exists at the expected path
2. List the contents of the archive to confirm all workspace files are included
3. Confirm setup.md is present at the root level

"**Archive verification:**
- File: `{system_name}.ocf.zip`
- Size: {file_size}
- Files included: {count}
- Setup prompt: ✅ included"

If verification fails, report the issue and attempt to recreate.

### 4. Present Completion Summary

"**Package export complete!**

---

**Output Files:**

**Archive:** `{ocfOutputFolder}/packages/{system_name}.ocf.zip`
Contains all workspace files + setup prompt in a portable format.

**Setup Prompt:** `{ocfOutputFolder}/packages/{system_name}.setup.md`
Standalone copy for quick reference without extracting the archive.

---

**Package Contents:**
- {count} workspace files
- 1 setup prompt
- OCF version: {ocf_version}

**To use this package:**
1. Share the `.ocf.zip` file with the target OpenClaw instance
2. The receiving agent follows `{system_name}.setup.md` to unpack and activate
3. OCF metadata enables future upgrade-path detection

---

**Workflow complete.** The workspace has been successfully packaged for portable distribution."

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- ZIP archive created at correct output path
- Archive contains all workspace files with correct relative paths
- Setup.md included in archive at root level
- Standalone setup.md copy in packages/ directory
- Archive contents verified
- Completion summary presented with clear output paths
- No absolute paths in archive

### ❌ SYSTEM FAILURE:

- Archive contains absolute paths
- Missing workspace files in archive
- Setup.md not included
- Archive not created at correct output path
- Not verifying archive contents
- Not presenting completion summary

**Master Rule:** This is the final step. Create archive, verify contents, present summary. The package must be portable — no absolute paths, no environment-specific references.
