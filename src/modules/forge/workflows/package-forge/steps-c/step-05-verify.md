---
name: 'step-05-verify'
description: 'Verify the .ocf.zip package integrity and report results'

forgeArtifactsPath: '{forge_artifacts}'
ocfFormatSpec: '../data/ocf-format-spec.md'
---

# Step 5: Verify Package

## STEP GOAL:

Verify the .ocf.zip package can be extracted, all files match the manifest, required files are present, and metadata is valid. Report the final build results.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a build system orchestrator performing quality assurance on the package
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ Thorough verification — every check matters

### Step-Specific Rules:

- 🎯 Focus only on verifying the archive
- 🚫 FORBIDDEN to modify the archive
- 💬 Report all verification results clearly

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Report verification results
- 📖 Reference {ocfFormatSpec} for verification checks
- 🚫 This is the final step — no next step to load

## CONTEXT BOUNDARIES:

- Available: Archive path, file manifest, metadata from previous steps
- Focus: Extraction, validation, and reporting
- Limits: Read-only — do not modify the archive
- Dependencies: Step 4 must have created the archive

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Verification Criteria

Load `{ocfFormatSpec}` to reference the verification checks.

### 2. Extract Archive

Extract `{forgeArtifactsPath}/forge-{version}.ocf.zip` to a temporary directory.

If extraction fails:

"**VERIFICATION FAILED: Archive cannot be extracted**
Error: {error details}

The package is corrupt and cannot be distributed."

HALT on extraction failure.

### 3. Verify manifest.json

Check the extracted manifest.json:

1. File exists at archive root
2. Valid JSON format
3. Required fields present: name, version, buildDate, compatibility, files, fileCount
4. Version matches the version provided in Step 1
5. fileCount matches actual number of files in the files array

Report:
"**manifest.json verification:**
- [x] File exists
- [x] Valid JSON
- [x] Required fields present
- [x] Version matches: {version}
- [x] File count matches: {count}"

### 4. Verify Required Files

Check that all required files from the format spec are present:

- manifest.json
- SETUP.md
- workspace/SOUL.md
- workspace/AGENTS.md
- workspace/IDENTITY.md

Report:
"**Required files verification:**
- [x] manifest.json
- [x] SETUP.md
- [x] workspace/SOUL.md
- [x] workspace/AGENTS.md
- [x] workspace/IDENTITY.md"

### 5. Verify File Completeness

Cross-reference every file in manifest.json with the actual extracted files:

1. Every file listed in manifest.json exists in the archive
2. No unexpected files exist that aren't in the manifest
3. File count matches

Report:
"**File completeness verification:**
- Listed in manifest: {count}
- Found in archive: {count}
- Missing: {count} — {list if any}
- Extra: {count} — {list if any}"

### 6. Final Report

"**Package Verification Report**

---

**Package:** forge-{version}.ocf.zip
**Location:** `{forgeArtifactsPath}/forge-{version}.ocf.zip`
**Size:** {size}
**Build Date:** {buildDate}

**Verification Results:**
| Check | Status |
|-------|--------|
| Archive extraction | PASS |
| manifest.json valid | PASS |
| Required files present | PASS |
| File completeness | PASS |
| Version match | PASS |

**Overall: PASS**

**Package Contents:**
- Workspace files: {count}
- Skill files: {count}
- Reference data: {count}
- Metadata files: {count}
- Total: {total}

---

**The Forge v{version} has been successfully packaged and is ready for distribution.**

Package location: `{forgeArtifactsPath}/forge-{version}.ocf.zip`"

If any checks failed:

"**Overall: FAIL**

**Failed checks:**
{list failed checks with details}

**The package should not be distributed until these issues are resolved.**"

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Archive successfully extracted
- manifest.json validates against schema
- All required files present
- File completeness verified
- Final report presented with PASS/FAIL status
- Build pipeline complete

### ❌ SYSTEM FAILURE:

- Not performing all verification checks
- Reporting PASS when checks failed
- Modifying the archive during verification
- Not presenting the final report

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
