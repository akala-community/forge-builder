---
name: 'step-04-update-patterns'
description: 'Update the agentic pattern library based on extraction findings'

nextStepFile: './step-05-update-config-ref.md'
extractionReportFile: '{output_folder}/extraction-report-{project_name}.md'
patternEntryTemplate: '../templates/pattern-entry.md'
patternOutputDir: '../data/patterns'
---

# Step 4: Update Pattern Library

## STEP GOAL:

To refresh the agentic pattern library reference files based on the extracted config schema and platform features, ensuring patterns reflect current OpenClaw capabilities.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a pattern library maintainer
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring expertise in agentic pattern design, user confirms which patterns to update
- ✅ Be precise — patterns must accurately reflect current platform capabilities

### Step-Specific Rules:

- 🎯 Focus only on updating pattern library — config reference is step 5
- 🚫 FORBIDDEN to modify config reference files in this step
- 💬 Use subprocess Pattern 2 for per-pattern generation when available
- ⚙️ If subprocess unavailable, generate patterns in main thread
- 💬 Present diff summary before writing — user must confirm changes

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Write updated pattern files to {patternOutputDir}
- 📖 Append update summary to {extractionReportFile}
- 🚫 FORBIDDEN to load next step until user confirms pattern updates

## CONTEXT BOUNDARIES:

- Available: Complete extraction report from steps 1-3
- Focus: Pattern library update based on extracted capabilities
- Limits: Do NOT update config reference yet
- Dependencies: Extraction report must have config schema and platform features

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Extraction Report and Current Patterns

Load {extractionReportFile} to get extracted config schema and platform features.

Check if {patternOutputDir} exists and has existing pattern files:
- **If existing patterns found:** Load them for comparison
- **If no existing patterns:** Will create from scratch

"**Preparing to update pattern library.**

**Extraction data loaded:**
- Config entries: {count}
- Platform features: {count}

**Current patterns:** {count existing or 'None — creating from scratch'}"

### 2. Identify Pattern Changes

Compare extracted capabilities against current patterns:

**Additions:** New capabilities not in current patterns
**Removals:** Current patterns referencing features no longer in source
**Updates:** Patterns that need adjustments for changed features

"**Pattern library changes identified:**

**New patterns to add:** {count}
{list new patterns}

**Patterns to remove (stale):** {count}
{list stale patterns}

**Patterns to update:** {count}
{list changed patterns with reason}"

### 3. Confirm Changes with User

"**Please review the proposed changes before I write them.**

Do these changes look correct? Any patterns I should skip or add?"

Wait for user confirmation.

### 4. Generate Updated Pattern Files

Load {patternEntryTemplate} for pattern file format.

DO NOT BE LAZY — For EACH pattern to create or update, launch a subprocess (or work in main thread) that:
1. Uses the pattern entry template
2. Fills in details from extraction data
3. Lists OpenClaw features used
4. Documents configuration requirements
5. Includes example usage
6. Writes the file to {patternOutputDir}

### 5. Remove Stale Patterns

For any patterns identified as stale (referencing removed features):
- Remove or archive the pattern file
- Document removal in extraction report

### 6. Append Update Summary

Append pattern update summary to {extractionReportFile} under `## Update Summary`:

```markdown
### Pattern Library Update
- Patterns added: {count} — {list}
- Patterns removed: {count} — {list}
- Patterns updated: {count} — {list}
- Total patterns: {count}
```

Update frontmatter: add `'step-04-update-patterns'` to `stepsCompleted`.

### 7. Present MENU OPTIONS

Display: "**Pattern library updated. Select:** [C] Continue to Config Reference Update"

#### Menu Handling Logic:

- IF C: Save update summary to {extractionReportFile}, update frontmatter, then load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then [Redisplay Menu Options](#7-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and pattern files are written and update summary is appended will you load {nextStepFile} to begin config reference update.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All current patterns compared against extracted data
- New patterns created for new capabilities
- Stale patterns removed
- Changed patterns updated
- User confirmed changes before writing
- Update summary appended to extraction report

### ❌ SYSTEM FAILURE:

- Writing patterns without user confirmation
- Missing new capabilities in pattern library
- Leaving stale references to removed features
- Not documenting changes in extraction report

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
