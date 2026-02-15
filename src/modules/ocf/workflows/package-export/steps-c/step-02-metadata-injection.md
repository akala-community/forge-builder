---
name: 'step-02-metadata-injection'
description: 'Inject OCF version and template metadata into workspace artifacts for upgrade-path tracking'

nextStepFile: './step-03-setup-prompt.md'
ocfModuleConfig: '{project-root}/src/modules/ocf/module.yaml'
---

# Step 2: Metadata Injection

## STEP GOAL:

To inject OCF version metadata and template origin tracking into workspace artifacts, enabling future upgrade-path detection.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are an assembly and packaging specialist (Cog / Gear Wright)
- ✅ Systematic, precise, methodical
- ✅ You bring metadata architecture and versioning expertise

### Step-Specific Rules:

- 🎯 Focus ONLY on injecting OCF metadata into workspace artifacts
- 🚫 FORBIDDEN to generate setup.md — that comes in step 03
- 🚫 FORBIDDEN to create the zip archive — that comes in step 04
- 💬 Report what was injected and where
- ⚙️ If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- 🎯 Determine OCF version to inject
- 💾 Inject metadata into workspace artifacts
- 📖 Track which files were modified
- 🚫 DO NOT alter the content or meaning of any artifact — metadata only

## CONTEXT BOUNDARIES:

- Workspace path, system name, and file inventory from step 01
- OCF version from module.yaml or user input
- Only adding metadata — not changing artifact content
- Dependencies: step 01 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Determine OCF Version

**If user specified a target OCF version in step 01:**
- Use the specified version

**If no version specified:**
- Read the OCF module version from `{ocfModuleConfig}` or use `6.0.0-Beta` as default
- Report the version being used

"**OCF Version:** `{ocf_version}` will be stamped into package metadata."

### 2. Prepare Metadata Block

Define the metadata to inject:

```yaml
# OCF Package Metadata
ocf_version: '{ocf_version}'
ocf_packaged: '{current_date}'
ocf_system_name: '{system_name}'
ocf_template_origins: '{list of template sources used during workspace creation, if detectable}'
```

### 3. Inject Metadata into AGENTS.md

Read the workspace's AGENTS.md file.

**If AGENTS.md has existing YAML frontmatter:**
- Add the OCF metadata fields to the existing frontmatter

**If AGENTS.md has no frontmatter:**
- Add a YAML frontmatter block at the top with the OCF metadata fields

Do not alter any existing content in the file.

### 4. Record Template Origins

Scan workspace artifacts for any template origin markers (comments or metadata indicating which OCF templates or workflows were used to create them).

Record these origins for inclusion in the setup.md and package metadata.

If no template origins are detectable, note "origins not tracked" — this is acceptable for manually created workspaces.

### 5. Report Injection Results

"**Metadata injection complete.**

**Files modified:**
- AGENTS.md — OCF metadata block added to frontmatter

**Metadata injected:**
- OCF Version: `{ocf_version}`
- Package Date: `{current_date}`
- System Name: `{system_name}`
- Template Origins: `{origins or 'not tracked'}`

**Proceeding to setup prompt generation...**"

Immediately load, read entire file, then execute {nextStepFile}.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- OCF version determined
- Metadata block injected into AGENTS.md
- Template origins recorded (or noted as untracked)
- No artifact content altered (metadata only)
- Auto-proceeding to step 03

### ❌ SYSTEM FAILURE:

- Altering artifact content beyond metadata
- Skipping metadata injection
- Not reporting what was modified
- Halting when should auto-proceed

**Master Rule:** This is a mechanical metadata step. Inject metadata precisely, report results, auto-proceed. DO NOT alter artifact content.
