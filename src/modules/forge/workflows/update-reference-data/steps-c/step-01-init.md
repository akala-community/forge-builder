---
name: 'step-01-init'
description: 'Locate and validate the OpenClaw source tree, create extraction report'

nextStepFile: './step-02-extract-config.md'
extractionReportFile: '{output_folder}/extraction-report-{project_name}.md'
extractionReportTemplate: '../templates/extraction-report.md'
---

# Step 1: Locate & Validate OpenClaw Source

## STEP GOAL:

To find the OpenClaw source tree, validate it has the expected structure, and create the extraction report that will collect findings across subsequent steps.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a systematic source code analyst
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring expertise in code parsing and source tree analysis, user brings knowledge of their OpenClaw setup
- ✅ Be methodical and precise — this is maintenance work, not creative work

### Step-Specific Rules:

- 🎯 Focus only on locating and validating the source tree
- 🚫 FORBIDDEN to extract config or features — that comes in steps 2-3
- 💬 Approach: Ask user for source path, validate, report findings

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Create extraction report from template when source is validated
- 📖 Update extraction report frontmatter with source information
- 🚫 This is the init step — sets up everything that follows

## CONTEXT BOUNDARIES:

- Available context: Workflow configuration from config.yaml
- Focus: Finding and validating the OpenClaw source tree
- Limits: Do NOT begin extraction — only validate source exists
- Dependencies: None — this is the first step

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Request OpenClaw Source Path

"**Let's update The Forge's reference data.**

First, I need to locate the OpenClaw source code.

**Please provide the path to the OpenClaw source root**, or I can try to auto-detect it from the current project."

**If user provides path:** Use that path.
**If user says auto-detect:** Look for OpenClaw indicators in the project root:
- Check for `package.json` with openclaw-related packages
- Check for `src/` directory structure typical of OpenClaw
- Check for `CLAUDE.md` or other OpenClaw markers

### 2. Validate Source Tree Structure

Once a path is identified, validate the source tree contains expected structure:

**Required indicators (at least 3 must be present):**
- `package.json` exists
- `src/` directory exists
- TypeScript/JavaScript source files present
- Configuration-related files exist (config schemas, type definitions)

**Report findings:**

"**Source tree validation:**

**Path:** {confirmed path}
**Status:** [Valid/Invalid]

**Found:**
- [x/o] package.json
- [x/o] src/ directory
- [x/o] TypeScript/JavaScript sources
- [x/o] Configuration files

**Source summary:** {brief description of source tree structure}"

**If invalid:** Ask user to verify path or provide alternative.

### 3. Create Extraction Report

Create {extractionReportFile} from {extractionReportTemplate} with:
- Set `sourceRoot` to the confirmed source path
- Set `date` to current date
- Set `openclawVersion` from package.json if available
- Set `stepsCompleted` to `['step-01-init']`

"**Extraction report created.** This will collect all findings as we scan the source."

### 4. Present MENU OPTIONS

Display: "**Source validated. Select:** [C] Continue to Config Schema Extraction"

#### Menu Handling Logic:

- IF C: Save source info to {extractionReportFile}, update frontmatter, then load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then [Redisplay Menu Options](#4-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and the extraction report is created with source information will you load {nextStepFile} to begin config schema extraction.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- OpenClaw source path confirmed and validated
- Source tree structure verified (at least 3 indicators present)
- Extraction report created from template
- Source information recorded in extraction report frontmatter
- User confirmed ready to proceed

### ❌ SYSTEM FAILURE:

- Proceeding without validating source tree
- Not creating extraction report
- Beginning extraction in this step (too early)
- Hardcoded paths instead of using {extractionReportFile}

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
