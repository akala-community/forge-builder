---
name: 'step-05-update-config-ref'
description: 'Update the config reference data files based on extraction findings'

nextStepFile: './step-06-validate.md'
extractionReportFile: '{output_folder}/extraction-report-{project_name}.md'
configRefEntryTemplate: '../templates/config-reference-entry.md'
configRefOutputDir: '../data/config-reference'
---

# Step 5: Update Config Reference

## STEP GOAL:

To write updated config reference data files based on the extracted config schema, ensuring all configuration entries are accurately documented for The Forge's config generation workflows.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a config reference maintainer
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring expertise in config documentation, user confirms accuracy
- ✅ Be exhaustive — every config entry must be documented

### Step-Specific Rules:

- 🎯 Focus only on config reference files — patterns were done in step 4
- 🚫 FORBIDDEN to modify pattern library files in this step
- 💬 Use subprocess Pattern 2 for per-section generation when available
- ⚙️ If subprocess unavailable, generate config refs in main thread
- 💬 Present diff summary before writing — user must confirm changes

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Write updated config reference files to {configRefOutputDir}
- 📖 Append update summary to {extractionReportFile}
- 🚫 FORBIDDEN to load next step until user confirms config ref updates

## CONTEXT BOUNDARIES:

- Available: Complete extraction report including config schema from step 2
- Focus: Config reference file update
- Limits: Do NOT modify pattern files
- Dependencies: Extraction report must have config schema

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Extraction Report and Current Config Reference

Load {extractionReportFile} to get extracted config schema.

Check if {configRefOutputDir} exists and has existing config reference files:
- **If existing files found:** Load them for comparison
- **If no existing files:** Will create from scratch

"**Preparing to update config reference.**

**Config schema entries from extraction:** {count}
**Current config reference files:** {count existing or 'None — creating from scratch'}"

### 2. Identify Config Reference Changes

Compare extracted config schema against current config reference:

**Additions:** New config entries not in current reference
**Removals:** Current references to config entries no longer in source
**Updates:** Config entries with changed types, defaults, or descriptions

"**Config reference changes identified:**

**New entries to add:** {count}
{list by category}

**Entries to remove (stale):** {count}
{list removed entries}

**Entries to update:** {count}
{list changed entries with what changed}"

### 3. Confirm Changes with User

"**Please review the proposed changes before I write them.**

Do these changes look correct? Any entries I should skip or add?"

Wait for user confirmation.

### 4. Generate Updated Config Reference Files

Load {configRefEntryTemplate} for config reference file format.

DO NOT BE LAZY — For EACH config section/category, launch a subprocess (or work in main thread) that:
1. Uses the config reference entry template
2. Fills in config key, type, default, description
3. Lists valid values and validation rules
4. Documents related config keys
5. Records source file and line number
6. Writes the file to {configRefOutputDir}

### 5. Remove Stale References

For any config references identified as stale:
- Remove or archive the reference file
- Document removal in extraction report

### 6. Append Update Summary

Append config reference update summary to {extractionReportFile} under `## Update Summary`:

```markdown
### Config Reference Update
- Entries added: {count} — {list}
- Entries removed: {count} — {list}
- Entries updated: {count} — {list}
- Total entries: {count}
```

Update frontmatter: add `'step-05-update-config-ref'` to `stepsCompleted`.

### 7. Present MENU OPTIONS

Display: "**Config reference updated. Select:** [C] Continue to Validation"

#### Menu Handling Logic:

- IF C: Save update summary to {extractionReportFile}, update frontmatter, then load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then [Redisplay Menu Options](#7-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and config reference files are written and update summary is appended will you load {nextStepFile} to begin cross-validation.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All config entries from extraction documented in reference files
- New entries created for new config options
- Stale references removed
- Changed entries updated with current information
- User confirmed changes before writing
- Update summary appended to extraction report

### ❌ SYSTEM FAILURE:

- Writing config refs without user confirmation
- Missing config entries from extraction
- Leaving stale references to removed config options
- Not documenting changes in extraction report

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
