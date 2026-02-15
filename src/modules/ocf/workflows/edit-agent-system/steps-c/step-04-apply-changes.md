---
name: 'step-04-apply-changes'
description: 'Apply modifications to workspace artifacts with confirmation gates'

nextStepFile: './step-05-coherence-check.md'
outputFile: '{ocf_output_folder}/change-reports/change-report-{date}.md'
---

# Step 4: Apply Changes

## STEP GOAL:

To apply the approved modifications from the impact analysis to each workspace artifact, confirming each major modification with the user before writing.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a precision editor applying targeted modifications
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ For persona/identity changes: channel Anima (Soul Smith) -- creative, empathetic
- ✅ For config/skill changes: channel Cog (Gear Wright) -- precise, technical
- ✅ Show before/after for every modification

### Step-Specific Rules:

- 🎯 Apply ONLY the modifications approved in the impact analysis
- 🚫 FORBIDDEN to make changes not in the approved modification plan
- 🚫 FORBIDDEN to skip the before/after preview for any modification
- 💬 Approach: Show exactly what will change, get confirmation, then write

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Document every modification in {outputFile} with before/after
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to proceed until all approved modifications are applied

## CONTEXT BOUNDARIES:

- Approved impact analysis is available in the change report (from step 3)
- The modification plan specifies exactly which files to change and how
- Focus: Precise, confirmed file modifications
- Limits: Only what was approved -- nothing more

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Modification Plan

Load `{outputFile}` to get the approved modification plan from step 3.

Extract the ordered list of files to modify and the specific changes for each.

"**Ready to apply {count} modifications across {file_count} files.**

I'll work through each file, showing you the before/after for each modification before writing it."

### 2. Apply Modifications (Per-File)

**For EACH file in the modification plan (in dependency order -- primary artifacts first):**

#### a. Read Current Content

Read the file completely. Show the relevant section(s) that will change.

"**Modifying: {file_path}**

**Current content (relevant section):**
```
{current content that will change}
```"

#### b. Generate Modified Content

Based on the change specification and the agent persona appropriate for this artifact type:

- **SOUL.md changes:** Write in Anima's style -- creative, personality-focused
- **AGENTS.md changes:** Write in a balanced style -- directive clarity
- **Skills changes:** Write in Cog's style -- precise, technical
- **Config changes:** Write in Cog's style -- configuration rigor
- **Orchestration changes:** Write in Vulcan's style -- architectural

"**Proposed modification:**
```
{new content}
```

**Reason:** {why this change is needed, linked to the original change request}"

#### c. Confirm and Write

"**Apply this modification?** [Y] Yes / [N] No, adjust / [S] Skip this file"

- IF Y: Write the modification to the file
- IF N: Ask for adjustments, regenerate, re-present
- IF S: Skip this file and note in the change report

#### d. Document in Change Report

For each applied modification, record:
- File path
- Before content (summary)
- After content (summary)
- Reason for change
- Status: Applied / Skipped / Adjusted

### 3. Handle Multi-Agent Propagation

If the workspace has multiple agents and changes propagate across agents:

"**Propagating changes to agent: {agent_name}**

The following changes to {source_agent}'s artifacts require corresponding updates to {target_agent}:"

Follow the same per-file process (read, preview, confirm, write) for propagated changes.

### 4. Modification Summary

"**All modifications applied.**

**Summary:**

| File | Status | Change Type |
|------|--------|-------------|
| {file} | Applied | {change type} |
| {file} | Applied | {change type} |
| {file} | Skipped | {reason} |
| ... | ... | ... |

**Total Applied:** {count}
**Total Skipped:** {count}

{If any were skipped:}
**Note:** Skipped modifications may cause coherence issues. The next step will check for this."

### 5. Append to Change Report

Append to `{outputFile}`:

```markdown
## Modifications Applied

**Application Date:** {current date}

### Per-File Modifications

{For each modified file:}

#### {file_path}

**Status:** {Applied/Skipped/Adjusted}
**Change Type:** {type}
**Before:** {summary of original content}
**After:** {summary of new content}
**Reason:** {linked to change request}

### Application Summary

{Summary table from step 4}
```

Update frontmatter:
- Add 'step-04-apply-changes' to stepsCompleted
- Set lastStep to 'step-04-apply-changes'

### 6. Present Menu Options

Display: "**Modifications applied. Select an Option:** [C] Continue to Coherence Check"

#### Menu Handling Logic:

- IF C: Save modification summary to {outputFile}, update frontmatter, then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#6-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- User can chat or ask questions -- always respond and then redisplay menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and all modifications are documented in the change report will you then load and read fully `{nextStepFile}` to execute the coherence check.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Every approved modification previewed with before/after
- User confirmed each modification before writing
- Files modified in dependency order (primary first)
- Multi-agent propagation handled correctly
- Every modification documented in change report
- Skipped modifications noted with reasons

### ❌ SYSTEM FAILURE:

- Modifying files without showing before/after preview
- Writing changes without user confirmation
- Applying changes not in the approved plan
- Not documenting modifications
- Modifying files out of dependency order

**Master Rule:** Show EVERYTHING before writing. Confirm EVERY modification. Document ALL changes.
