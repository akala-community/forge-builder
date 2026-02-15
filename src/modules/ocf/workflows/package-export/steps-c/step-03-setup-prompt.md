---
name: 'step-03-setup-prompt'
description: 'Generate the companion setup.md document from template and workspace contents'

nextStepFile: './step-04-package-assembly.md'
setupPromptTemplate: '../data/setup-prompt-template.md'
ocfOutputFolder: '{ocf_output_folder}'
---

# Step 3: Setup Prompt Generation

## STEP GOAL:

To generate the companion `{system_name}.setup.md` document that provides step-by-step instructions for an OpenClaw agent to unpack and activate the exported system.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are an assembly and packaging specialist (Cog / Gear Wright)
- ✅ Systematic, precise, methodical
- ✅ You bring expertise in documentation and installation procedures

### Step-Specific Rules:

- 🎯 Focus ONLY on generating the setup.md document
- 🚫 FORBIDDEN to create the zip archive — that comes in step 04
- 💬 Present the generated setup.md for user review before proceeding
- ⚙️ If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- 🎯 Load and populate the setup prompt template
- 💾 Write the populated setup.md to the output location
- 📖 Present for review and get confirmation
- 🚫 DO NOT proceed without user confirmation

## CONTEXT BOUNDARIES:

- Workspace path, system name, file inventory from step 01
- OCF metadata from step 02
- Custom setup instructions from step 01 (if any)
- Dependencies: steps 01 and 02 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Setup Prompt Template

Load {setupPromptTemplate} to get the template structure.

Read the template completely to understand all required variables.

### 2. Extract System Description

Read SOUL.md and/or AGENTS.md from the workspace to extract:
- A brief system description (1-2 sentences describing what this agent system does)
- Key personality traits or capabilities

If no clear description is found, ask the user:

"**I couldn't extract a clear system description from your workspace artifacts. Please provide a brief description (1-2 sentences) of what this agent system does:**"

### 3. Build File Manifest

Create a formatted file manifest listing every file in the workspace:

```markdown
### Root Files
- AGENTS.md
- SOUL.md
- USER.md
- [other files found]

### Directories
- skills/
  - [files within]
- memory/
  - [files within]

### Configuration
- openclaw.json
```

Include relative paths only — no absolute paths.

### 4. Populate Template

Replace all template variables with actual values:

| Variable | Value |
|----------|-------|
| `{{ocf_version}}` | From step 02 metadata |
| `{{system_name}}` | From step 01 |
| `{{system_description}}` | From step 03 extraction |
| `{{creation_date}}` | Current date (ISO format) |
| `{{file_manifest}}` | From step 03 manifest |
| `{{template_origins}}` | From step 02 |
| `{{custom_instructions}}` | From step 01 user input (or empty) |

### 5. Write Setup.md

Write the populated setup.md to:
`{ocfOutputFolder}/packages/{system_name}.setup.md`

Create the `packages/` directory if it doesn't exist.

### 6. Present for Review

"**Setup prompt generated.**

**File:** `{ocfOutputFolder}/packages/{system_name}.setup.md`

Here's a summary of what was generated:"

Present the key sections:
- System overview (name, description, version)
- File manifest (count of files)
- Activation procedure highlights
- Custom instructions (if any)

"**Please review the setup prompt. When satisfied:**

**Select:** [C] Continue to package assembly"

#### Menu Handling Logic:

- IF C: Load, read entire file, then execute {nextStepFile}
- IF Any other: help user refine the setup.md, then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Template loaded and all variables populated
- System description extracted or obtained from user
- File manifest complete with all workspace files
- Setup.md written to correct output location
- User reviewed and confirmed the setup prompt
- Proceeding to package assembly

### ❌ SYSTEM FAILURE:

- Using absolute paths in file manifest
- Missing template variables (unpopulated placeholders)
- Not presenting setup.md for review
- Proceeding without user confirmation
- Creating zip archive in this step

**Master Rule:** Generate setup.md from template, present for review, get confirmation. DO NOT proceed without user approval.
