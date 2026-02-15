---
name: 'step-02-extract-config'
description: 'Extract configuration schema from OpenClaw source code'

nextStepFile: './step-03-extract-features.md'
extractionReportFile: '{output_folder}/extraction-report-{project_name}.md'
extractionTargetsData: '../data/extraction-targets.md'
---

# Step 2: Extract Config Schema

## STEP GOAL:

To parse the OpenClaw source code and extract all configuration schema entries including config keys, types, defaults, model config, and binding/integration config.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a systematic source code analyst specializing in config extraction
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring expertise in TypeScript/JavaScript parsing, user confirms accuracy of findings
- ✅ Be methodical — extract everything, miss nothing

### Step-Specific Rules:

- 🎯 Focus only on config schema extraction — not platform features (that's step 3)
- 🚫 FORBIDDEN to update pattern library or config reference files — that's steps 4-5
- 💬 Use subprocess Pattern 2 for per-file deep analysis when available
- 💬 Subprocess returns structured extraction findings, not full file contents
- ⚙️ If subprocess unavailable, perform analysis in main thread

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append extracted config schema to {extractionReportFile}
- 📖 Update extraction report frontmatter stepsCompleted
- 🚫 FORBIDDEN to load next step until extraction is confirmed

## CONTEXT BOUNDARIES:

- Available: Source path from step 1 (in extraction report frontmatter)
- Focus: Config schema only — types, defaults, validation rules
- Limits: Do NOT extract platform features yet
- Dependencies: Extraction report must exist from step 1

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Extraction Targets

Load {extractionTargetsData} and identify the Config Schema Targets section.

"**Beginning config schema extraction.**

I'll scan the OpenClaw source for configuration schema across these categories:
1. Model Configuration
2. Hook Configuration
3. Memory/State Configuration
4. Spawn/Process Configuration
5. Permission Configuration
6. MCP Server Configuration
7. Auth/Identity Configuration"

### 2. Scan Source for Config Files

Load the extraction report to get the source root path.

Search the source tree for config-related files matching the patterns from {extractionTargetsData}:
- `**/openclaw.json` or similar config files
- `**/config.ts`, `**/config.js` — Config type definitions
- `**/schema.ts`, `**/schema.js` — JSON schema definitions
- `**/types.ts` — TypeScript type definitions for config

"**Found config-related files:**
{list each file found with brief description}"

### 3. Extract Config Schema (Per-File Analysis)

DO NOT BE LAZY — For EACH config-related file found, launch a subprocess (or analyze in main thread) that:
1. Loads the file completely
2. Identifies all config keys, their types, defaults, and validation rules
3. Categorizes each entry (model, hook, memory, spawn, permission, MCP, auth)
4. Returns structured findings in this format:

```yaml
- name: config_key_name
  type: string|number|boolean|object|array
  description: what this config does
  default: default value
  required: true|false
  category: model|hook|memory|spawn|permission|mcp|auth
  source_file: path/to/file.ts
  source_line: line number
```

### 4. Compile and Present Findings

Aggregate all findings and present to user:

"**Config Schema Extraction Complete**

**Summary:**
- Total config entries found: {count}
- By category:
  - Model: {count}
  - Hook: {count}
  - Memory: {count}
  - Spawn: {count}
  - Permission: {count}
  - MCP: {count}
  - Auth: {count}

**Details:**
{Present organized list of all config entries by category}"

### 5. Append to Extraction Report

Append the extracted config schema to {extractionReportFile} under the `## Config Schema` section.

Update frontmatter: add `'step-02-extract-config'` to `stepsCompleted`.

### 6. Present MENU OPTIONS

Display: "**Config extraction complete. Select:** [C] Continue to Platform Feature Extraction"

#### Menu Handling Logic:

- IF C: Save extraction to {extractionReportFile}, update frontmatter, then load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then [Redisplay Menu Options](#6-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and all config schema has been appended to the extraction report will you load {nextStepFile} to begin platform feature extraction.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All config-related source files scanned
- Config entries extracted with type, default, description, source location
- Entries categorized correctly
- Findings appended to extraction report
- User confirmed extraction results

### ❌ SYSTEM FAILURE:

- Missing config files (not scanning broadly enough)
- Incomplete extraction (skipping entries)
- Extracting platform features in this step (too early)
- Not appending to extraction report
- Lazy analysis — skipping files or rushing through them

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
