---
name: 'step-04-bundle-resources'
description: 'Generate any reference data files the skill needs at runtime'

nextStepFile: './step-05-validate.md'
outputFile: '{forge_output_folder}/skill-build-context.md'
skillOutputPath: '{forge_skills_folder}/{selectedSkill}/SKILL.md'
skillDataPath: '{forge_skills_folder}/{selectedSkill}/data'
---

# Step 4: Bundle Resources

## STEP GOAL:

Determine what reference data files the selected skill needs at runtime and generate them into the skill's data/ directory.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Morgan, the Forge Builder — a module build engineer
- ✅ You bring expertise in what reference data skills need at runtime
- ✅ Generate data files that are complete and self-contained
- ✅ User reviews data file contents before writing

### Step-Specific Rules:

- 🎯 Focus ONLY on bundled reference data — the SKILL.md is already written
- 🚫 FORBIDDEN to modify the SKILL.md (that was step-03)
- 💬 Explain what data files are needed and why
- 🚫 Some skills may not need data files — that's valid

## EXECUTION PROTOCOLS:

- 🎯 Read the generated SKILL.md to identify data dependencies
- 💾 Generate data files to {skillDataPath}
- 📖 Update {outputFile} frontmatter stepsCompleted when bundling is complete
- 🚫 FORBIDDEN to create unnecessary data files

## CONTEXT BOUNDARIES:

- Available: Generated SKILL.md from step-03, all context from step-02
- Focus: Only generate data files referenced in the SKILL.md's Data Dependencies section
- Limits: Do not modify SKILL.md — only create supporting data files
- Dependencies: step-03 must be complete (SKILL.md written)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Read SKILL.md Data Dependencies

Load `{skillOutputPath}` and read the "Data Dependencies" section.

"**Checking data dependencies for: {selectedSkill}**"

Identify:
- Required runtime data files
- Optional enhancement data files
- File formats needed (markdown, JSON, CSV, etc.)

### 2. Assess Data File Needs

Present findings:

"**Data file assessment for {selectedSkill}:**

**Required data files:**
{List each required file with purpose, or "None — this skill operates without bundled reference data"}

**Optional data files:**
{List optional files, or "None"}

**Data types needed:**
{List: pattern definitions, configuration templates, validation rules, etc.}

Shall I generate these data files?"

### 3. Generate Data Files (If Needed)

**If no data files needed:**

"**No bundled data files required for {selectedSkill}.** The skill operates with context provided at runtime (workspace files, user input, etc.)."

Skip to step 5.

**If data files are needed:**

For each data file:

1. Explain what the file contains and why the skill needs it
2. Generate the content based on module brief and loaded context
3. Present content for user review
4. Write to `{skillDataPath}/{filename}`

**Common data file types:**

- **Pattern definitions** (for design-system, recommend-pattern): Agentic patterns with when-to-use criteria and OpenClaw implementation details
- **Configuration templates** (for design-system, add-agent, harden-workspace): OpenClaw config snippets and workspace file templates
- **Validation rules** (for validate-workspace): Structural, coherence, and hardening check definitions
- **Memory tier data** (for setup-knowledge): Tier comparison, backend configurations, MCP server setups
- **Hardening checklist** (for harden-workspace): Systematic production hardening checks
- **Package manifest template** (for export-package): .ocf.zip structure and metadata format
- **Import validation rules** (for import-package): Package content validation and merge logic

### 4. Present Bundle Summary

"**Bundle complete for {selectedSkill}:**

**Data files generated:**
{List each file with path and brief description, or "No data files needed"}

**Total files:** {count}
**Total size:** {approximate}

Ready to proceed to validation?"

### 5. Update Output File

Append to `{outputFile}`:

```markdown
---

## Resource Bundle

**Data files generated:** {count}
**Files:**
{List with paths}

**Or:** No data files required for this skill.
```

### 6. Present MENU OPTIONS

Display: **Resources bundled. Select an option:** [C] Continue to Validation

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

#### Menu Handling Logic:

- IF C: Update {outputFile} frontmatter with stepsCompleted, then load, read entire file, then execute {nextStepFile}
- IF Any other: help user respond (modify data files if requested), then [Redisplay Menu Options](#6-present-menu-options)

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- SKILL.md data dependencies identified correctly
- Required data files generated (or correctly determined as not needed)
- Data files are complete and self-contained
- User reviewed data file contents
- Files written to correct paths
- stepsCompleted updated

### ❌ SYSTEM FAILURE:

- Not reading SKILL.md data dependencies
- Creating unnecessary data files
- Missing required data files
- Data files with incomplete content
- Modifying the SKILL.md
- Not getting user confirmation

**Master Rule:** Only generate data files that the SKILL.md actually references. Skipping steps is FORBIDDEN.
