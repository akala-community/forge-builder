---
name: 'step-02-collect'
description: 'Scan workspace and collect all files to include in the package'

nextStepFile: './step-03-metadata.md'
forgeWorkspacePath: '{forge_artifacts}'
---

# Step 2: Collect Artifacts

## STEP GOAL:

Scan the Forge workspace and build a complete manifest of all files that will be included in the .ocf.zip package, organized by category (workspace, skills, reference).

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a build system orchestrator collecting artifacts for packaging
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ Systematic and thorough — every file must be accounted for

### Step-Specific Rules:

- 🎯 Focus only on enumerating and categorizing files
- 🚫 FORBIDDEN to modify any files or create the archive
- 💬 Report findings clearly with file counts and categories

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Build a complete file manifest in memory
- 📖 Categorize every file by type
- 🚫 Do not skip any files in the workspace

## CONTEXT BOUNDARIES:

- Available: Version number, workspace path, validation results from Step 1
- Focus: File discovery and categorization
- Limits: Do not modify files or start packaging
- Dependencies: Step 1 must have passed validation

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Collect Workspace Files

Scan `{forgeWorkspacePath}` for core workspace documents:

- SOUL.md
- AGENTS.md
- IDENTITY.md
- Any other .md files in the workspace root

For each file found, record:
- File path (relative to workspace root)
- File size
- Category: "workspace"

### 2. Collect Skill Files

Scan for skill files (typically in a skills subdirectory or matching skill patterns):

- `skills/**/*.md`
- `skills/**/*.yaml`
- Any other skill-related files

For each file found, record:
- File path
- File size
- Category: "skills"

### 3. Collect Reference Data

Scan for reference data:

- `reference/**/*` or `data/**/*`
- Patterns library files
- Configuration reference files

For each file found, record:
- File path
- File size
- Category: "reference"

### 4. Build Manifest Summary

"**Artifact Collection Complete**

**Workspace files:** {count}
{list each file}

**Skill files:** {count}
{list each file}

**Reference data:** {count}
{list each file}

**Total files:** {total_count}
**Total size:** {total_size}

All artifacts collected and categorized."

### 5. Proceed to Metadata

"**Proceeding to metadata injection...**"

#### Menu Handling Logic:

- After manifest is built, immediately load, read entire file, then execute {nextStepFile}

#### EXECUTION RULES:

- This is an auto-proceed step — deterministic file scan
- Proceed directly to next step after collection is complete

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN all artifacts are collected and the manifest is built will you load and read fully `{nextStepFile}` to begin metadata injection.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All workspace files discovered and categorized
- All skill files discovered and categorized
- All reference data discovered and categorized
- Complete manifest built with file paths, sizes, and categories
- Proceeding to step 3

### ❌ SYSTEM FAILURE:

- Missing files from the scan
- Not categorizing files properly
- Modifying files during collection
- Starting to create the archive

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
