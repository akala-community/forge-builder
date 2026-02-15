---
name: 'step-03-install-files'
description: 'Copy workspace files from extracted package to target directory, handle conflicts'

nextStepFile: './step-04-merge-config.md'
---

# Step 3: Install Files

## STEP GOAL:

To copy all workspace files from the extracted package to the target workspace directory, handling any conflicts with existing files by asking the user for resolution (overwrite, merge, or skip).

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step, ensure entire file is read
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are an installation specialist (Cog / Gear Wright)
- Systematic, precise, methodical
- You bring expertise in workspace file management and safe installation

### Step-Specific Rules:

- Focus ONLY on copying workspace files to the target directory
- FORBIDDEN to merge openclaw.json configuration - that comes in step 04
- Handle openclaw.json by copying it alongside (not merging) for step 04 to process
- Present conflict resolution options for each conflicting file
- If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- Create target directory structure if needed
- Copy workspace root files to target
- Copy skills directory contents to target
- Copy memory directory contents to target
- Handle each conflict individually with user input
- Record all installation actions for the completion report
- DO NOT merge openclaw.json - only copy it for step 04

## CONTEXT BOUNDARIES:

- Extracted package contents from step 01
- Target workspace path from step 01
- Validation results and conflict list from step 02
- Dependencies: steps 01 and 02 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Prepare Target Directory

Ensure the target workspace directory exists. Create it if necessary.

Ensure required subdirectories exist:
- `{target_path}/skills/` (if the package contains skills)
- `{target_path}/memory/` (if the package contains memory files)

"**Preparing target workspace:** `{target_path}`"

### 2. Install Root Workspace Files

For each root-level workspace file in the package (AGENTS.md, SOUL.md, USER.md, IDENTITY.md, TOOLS.md, HEARTBEAT.md, MEMORY.md, BOOT.md, and any other root markdown files):

**If no conflict exists:**
- Copy the file to `{target_path}/{filename}`
- Record: "Installed {filename}"

**If a conflict exists (file already present at target):**
- Present the conflict to the user:

"**Conflict:** `{filename}` already exists in the target workspace.

**Options:**
- [O] Overwrite - Replace the existing file with the package version
- [S] Skip - Keep the existing file, do not install the package version
- [D] Diff - Show differences between existing and package versions before deciding

**Select an option for `{filename}`:**"

Wait for user input.

- IF O: Overwrite the existing file. Record: "Overwritten {filename}"
- IF S: Skip the file. Record: "Skipped {filename} (existing kept)"
- IF D: Show a comparison of the two files (key differences), then re-present the O/S choice

**Do NOT present conflict options for openclaw.json** - set it aside for step 04. Record: "openclaw.json deferred to config merge step"

### 3. Install Skills Directory

If the package contains a `skills/` directory:

For each file in `skills/`:

**If no conflict exists:**
- Copy to `{target_path}/skills/{filename}`
- Record: "Installed skills/{filename}"

**If a conflict exists:**
- Present the same conflict resolution menu as in section 2 (O/S/D options)
- Apply the user's choice

"**Skills installed:** {count} files"

### 4. Install Memory Directory

If the package contains a `memory/` directory:

For each file in `memory/`:

**If no conflict exists:**
- Copy to `{target_path}/memory/{filename}`
- Record: "Installed memory/{filename}"

**If a conflict exists:**
- Present the same conflict resolution menu (O/S/D options)
- Apply the user's choice

"**Memory files installed:** {count} files"

### 5. Install Other Directories

If the package contains any other directories not yet handled, install them using the same pattern (create target subdirectory, copy files, handle conflicts).

### 6. Present Installation Summary

"**File Installation Summary**

---

**Installed:**
{list each file that was installed or overwritten}

**Skipped:**
{list each file that was skipped, or 'None'}

**Deferred:**
- openclaw.json (will be merged in next step)

**Total:** {installed_count} installed, {skipped_count} skipped, {deferred_count} deferred

---

**Proceeding to configuration merge...**"

Auto-proceed: Load, read entire file, then execute {nextStepFile}.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Target directory structure created
- All non-conflicting files installed to correct paths
- Each conflict presented to user with clear options
- User's conflict resolution choices applied correctly
- openclaw.json deferred to step 04 (not merged here)
- Installation actions recorded for completion report
- Auto-proceeding to configuration merge

### FAILURE:

- Not creating target directory structure
- Overwriting files without asking for conflict resolution
- Merging openclaw.json in this step
- Not recording installation actions
- Skipping files silently without user input
- Not presenting installation summary

**Master Rule:** Install files safely with proper conflict handling. Copy openclaw.json but DO NOT merge it. Record every action taken.
