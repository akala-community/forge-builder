---
name: 'step-03-metadata'
description: 'Inject package metadata and generate first-run setup prompt'

nextStepFile: './step-04-bundle.md'
ocfFormatSpec: '../data/ocf-format-spec.md'
---

# Step 3: Metadata & Setup Prompt

## STEP GOAL:

Create the package metadata (manifest.json) with version, build date, and compatibility info, and generate the SETUP.md first-run setup instructions for the installer.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a build system orchestrator creating package metadata
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ Precise and structured — metadata must be exact

### Step-Specific Rules:

- 🎯 Focus only on creating metadata and setup instructions
- 🚫 FORBIDDEN to create the archive — that's step 4
- 💬 Generate metadata deterministically from collected manifest data

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Create manifest.json and SETUP.md content
- 📖 Reference {ocfFormatSpec} for format requirements
- 🚫 Do not start bundling

## CONTEXT BOUNDARIES:

- Available: Version number, file manifest from Step 2, format spec
- Focus: Metadata creation and setup prompt generation
- Limits: Do not create archive or modify source files
- Dependencies: Step 2 must have completed artifact collection

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Format Specification

Load `{ocfFormatSpec}` to reference the manifest.json schema and required metadata fields.

### 2. Generate manifest.json

Create the manifest.json content following the schema from the format spec:

```json
{
  "name": "forge",
  "version": "{version from step 1}",
  "buildDate": "{current ISO 8601 timestamp}",
  "compatibility": {
    "openclaw": ">=1.0.0"
  },
  "files": [
    {
      "path": "{relative path within archive}",
      "type": "{workspace|skills|reference}",
      "required": true/false
    }
  ],
  "fileCount": {total from manifest},
  "checksum": ""
}
```

Populate the files array from the manifest built in Step 2. Mark workspace core files (SOUL.md, AGENTS.md, IDENTITY.md) as required.

### 3. Generate SETUP.md

Create the first-run setup prompt:

```markdown
# Forge Setup

## Installation Complete

The Forge v{version} has been installed successfully.

## First-Run Configuration

### 1. Review Your Workspace

The following files have been installed:

**Core Workspace:**
{list workspace files}

**Skills:**
{list skill files}

**Reference Data:**
{list reference files}

### 2. Configure Your Environment

1. Review SOUL.md and customize the agent identity for your project
2. Review AGENTS.md and adjust agent definitions as needed
3. Update IDENTITY.md with your system-specific configuration

### 3. Verify Installation

Run the validate-forge workflow to ensure all components are properly configured.

---

*Built on {buildDate} | Forge v{version}*
```

### 4. Generate RELEASE.md (If Applicable)

If release notes were provided in Step 1:

Create RELEASE.md content:
```markdown
# Forge v{version} Release Notes

**Release Date:** {buildDate}

{user-provided release notes content}

---

{changelog content if provided}
```

If no release notes were provided, skip this.

### 5. Report Metadata Status

"**Metadata generation complete:**
- manifest.json — created ({fileCount} files indexed)
- SETUP.md — created (first-run instructions)
- RELEASE.md — {created/skipped}

**Proceeding to archive bundling...**"

### 6. Proceed to Bundle

#### Menu Handling Logic:

- After metadata is generated, immediately load, read entire file, then execute {nextStepFile}

#### EXECUTION RULES:

- This is an auto-proceed step — deterministic metadata generation
- Proceed directly to next step after completion

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN manifest.json and SETUP.md are generated will you load and read fully `{nextStepFile}` to begin archive bundling.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- manifest.json created with all required fields
- All files from manifest indexed in manifest.json
- SETUP.md created with first-run instructions
- RELEASE.md created if release notes were provided
- Proceeding to step 4

### ❌ SYSTEM FAILURE:

- Missing fields in manifest.json
- Files from manifest not indexed
- Invalid JSON in manifest.json
- Starting to create the archive

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
