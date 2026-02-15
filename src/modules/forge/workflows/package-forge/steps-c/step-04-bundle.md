---
name: 'step-04-bundle'
description: 'Create the .ocf.zip archive from collected artifacts and metadata'

nextStepFile: './step-05-verify.md'
forgeArtifactsPath: '{forge_artifacts}'
ocfFormatSpec: '../data/ocf-format-spec.md'
---

# Step 4: Bundle .ocf.zip

## STEP GOAL:

Create the .ocf.zip archive containing all collected workspace files, skill files, reference data, metadata (manifest.json), setup prompt (SETUP.md), and optional release notes (RELEASE.md), organized according to the .ocf.zip format specification.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a build system orchestrator creating the distributable package
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ Precise file operations — archive must be correct

### Step-Specific Rules:

- 🎯 Focus only on creating the .ocf.zip archive
- 🚫 FORBIDDEN to modify source files
- 💬 Report progress during bundling

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Create archive at `{forgeArtifactsPath}/forge-{version}.ocf.zip`
- 📖 Follow archive structure from {ocfFormatSpec}
- 🚫 Do not verify the archive — that's step 5

## CONTEXT BOUNDARIES:

- Available: File manifest, metadata content, setup prompt, optional release notes
- Focus: Archive creation with correct directory structure
- Limits: Do not modify source files, do not verify archive
- Dependencies: Step 3 must have completed metadata generation

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Prepare Archive Structure

Create a temporary staging directory with the .ocf.zip internal structure:

```
staging/
├── manifest.json
├── SETUP.md
├── workspace/
│   ├── SOUL.md
│   ├── AGENTS.md
│   ├── IDENTITY.md
│   └── [other workspace files]
├── skills/
│   └── [skill files]
├── reference/
│   ├── patterns/
│   └── config/
└── RELEASE.md  (if provided)
```

### 2. Copy Files to Staging

For each file in the manifest:

1. Determine target path within the archive based on category:
   - workspace → `workspace/{filename}`
   - skills → `skills/{relative_path}`
   - reference → `reference/{relative_path}`

2. Read source file content
3. Write to staging directory at the target path

Write manifest.json and SETUP.md to staging root.
Write RELEASE.md to staging root if release notes were provided.

### 3. Create Archive

Create the zip archive at `{forgeArtifactsPath}/forge-{version}.ocf.zip` containing all files from the staging directory.

Report progress:

"**Bundling .ocf.zip...**
- Writing workspace files... ({count})
- Writing skill files... ({count})
- Writing reference data... ({count})
- Writing metadata...
- Writing setup prompt...
{if release notes} - Writing release notes... {end if}

**Archive created:** `{forgeArtifactsPath}/forge-{version}.ocf.zip`"

### 4. Write RELEASE.md (If Applicable)

If release notes were provided, also write a standalone RELEASE.md to `{forgeArtifactsPath}/RELEASE.md` alongside the archive.

### 5. Report Bundle Status

"**Bundle complete:**
- Archive: `{forgeArtifactsPath}/forge-{version}.ocf.zip`
- Size: {archive_size}
- Files included: {file_count}

**Proceeding to verification...**"

### 6. Proceed to Verify

#### Menu Handling Logic:

- After archive is created, immediately load, read entire file, then execute {nextStepFile}

#### EXECUTION RULES:

- This is an auto-proceed step — deterministic archive creation
- Proceed directly to next step after archive is created

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN the .ocf.zip archive is created at `{forgeArtifactsPath}/forge-{version}.ocf.zip` will you load and read fully `{nextStepFile}` to begin verification.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Archive created at correct path
- All files from manifest included in archive
- Archive follows .ocf.zip directory structure
- manifest.json and SETUP.md at archive root
- Standalone RELEASE.md written if applicable
- Proceeding to step 5

### ❌ SYSTEM FAILURE:

- Archive not created
- Missing files from archive
- Wrong directory structure
- Modifying source files
- Starting verification in this step

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
