---
name: 'step-03-extract-features'
description: 'Extract platform features from OpenClaw source code'

nextStepFile: './step-04-update-patterns.md'
extractionReportFile: '{output_folder}/extraction-report-{project_name}.md'
extractionTargetsData: '../data/extraction-targets.md'
---

# Step 3: Extract Platform Features

## STEP GOAL:

To identify and extract all platform features from the OpenClaw source including hooks, spawn config, memory backends, permission system, and tool system.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a platform capability analyst
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring expertise in identifying system capabilities from source code, user confirms accuracy
- ✅ Be thorough — document every feature available on the platform

### Step-Specific Rules:

- 🎯 Focus only on platform feature extraction — config schema was done in step 2
- 🚫 FORBIDDEN to update pattern library or config reference — that's steps 4-5
- 💬 Use subprocess Pattern 2 for per-file deep analysis when available
- 💬 Subprocess returns structured feature findings, not full file contents
- ⚙️ If subprocess unavailable, perform analysis in main thread

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append extracted features to {extractionReportFile}
- 📖 Update extraction report frontmatter stepsCompleted
- 🚫 FORBIDDEN to load next step until extraction is confirmed

## CONTEXT BOUNDARIES:

- Available: Source path and config schema from steps 1-2 (in extraction report)
- Focus: Platform features — hooks, spawn, memory, permissions, tools
- Limits: Do NOT update reference data yet
- Dependencies: Extraction report with config schema from step 2

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Extraction Targets

Load {extractionTargetsData} and identify the Platform Feature Targets section.

"**Beginning platform feature extraction.**

I'll scan the OpenClaw source for platform capabilities:
1. Hook System — types, lifecycle, registration
2. Spawn/Subprocess System — config, workers, parallelization
3. Memory Backends — providers, state storage, persistence
4. Permission System — definitions, access control, capabilities
5. Tool System — definitions, registry, available tools"

### 2. Scan Source for Feature Files

Search the source tree for feature-related files matching patterns from {extractionTargetsData}:

**Hook System:**
- `**/hooks/**`, `hook.ts`, `hook-*.ts`, patterns containing `*Hook*`

**Spawn/Subprocess:**
- `**/spawn/**`, `subprocess.ts`, `worker.ts`

**Memory Backends:**
- `**/memory/**`, `**/state/**`, patterns containing `*Provider*`

**Permission System:**
- `**/permissions/**`, `**/access/**`, `permission*.ts`

**Tool System:**
- `**/tools/**`, `tool-*.ts`, patterns containing `*Tool*`

"**Found feature-related files:**
{list each file found with its feature category}"

### 3. Extract Platform Features (Per-File Analysis)

DO NOT BE LAZY — For EACH feature-related file found, launch a subprocess (or analyze in main thread) that:
1. Loads the file completely
2. Identifies all feature definitions, types, and interfaces
3. Extracts feature signatures, parameters, and capabilities
4. Returns structured findings:

```yaml
- name: feature_name
  type: hook|spawn|memory|permission|tool
  description: what this feature provides
  interface: function signature or API
  config_keys: related config entries
  source_file: path/to/file.ts
  source_line: line number
```

### 4. Compile and Present Findings

"**Platform Feature Extraction Complete**

**Summary:**
- Total features found: {count}
- By type:
  - Hooks: {count} — {list names}
  - Spawn: {count} — {list names}
  - Memory: {count} — {list names}
  - Permissions: {count} — {list names}
  - Tools: {count} — {list names}

**Details:**
{Present organized list of all features by type}"

### 5. Append to Extraction Report

Append the extracted features to {extractionReportFile} under the `## Platform Features` section.

Update frontmatter: add `'step-03-extract-features'` to `stepsCompleted`.

### 6. Present MENU OPTIONS

Display: "**Feature extraction complete. Select:** [C] Continue to Pattern Library Update"

#### Menu Handling Logic:

- IF C: Save extraction to {extractionReportFile}, update frontmatter, then load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then [Redisplay Menu Options](#6-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and all features have been appended to the extraction report will you load {nextStepFile} to begin updating the pattern library.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All feature-related source files scanned
- Features extracted with type, description, interface, config relationships
- Findings appended to extraction report
- User confirmed extraction results

### ❌ SYSTEM FAILURE:

- Missing feature categories (not scanning broadly enough)
- Incomplete feature extraction
- Updating reference data in this step (too early)
- Not appending to extraction report

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
