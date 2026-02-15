---
name: 'step-03-generate-skill'
description: 'Generate the complete SKILL.md content from accumulated context'

nextStepFile: './step-04-bundle-resources.md'
outputFile: '{forge_output_folder}/skill-build-context.md'
skillOutputPath: '{forge_skills_folder}/{selectedSkill}/SKILL.md'
---

# Step 3: Generate SKILL.md

## STEP GOAL:

Generate the complete SKILL.md definition for the selected skill, including triggers, execution flow, instructions, and all required sections.

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
- ✅ You bring expertise in OpenClaw skill architecture and SKILL.md format
- ✅ Generate content that is complete, precise, and consistent with the module brief
- ✅ User reviews and approves the generated content

### Step-Specific Rules:

- 🎯 Focus on generating SKILL.md from the loaded context
- 🚫 FORBIDDEN to skip any required SKILL.md section
- 💬 Present generated content for user review before writing
- 🚫 FORBIDDEN to write the file without user confirmation

## EXECUTION PROTOCOLS:

- 🎯 Read all accumulated context from {outputFile}
- 💾 Generate SKILL.md and write to {skillOutputPath}
- 📖 Update {outputFile} frontmatter stepsCompleted when generation confirmed
- 🚫 FORBIDDEN to proceed without user confirmation of generated content

## CONTEXT BOUNDARIES:

- Available: All context loaded in step-02 (module brief extract, skill registry, patterns)
- Focus: Generate a complete, valid SKILL.md
- Limits: Only generate for the selected skill — do not generate data files (that's step-04)
- Dependencies: step-02 context must be loaded in output file

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Read Accumulated Context

Load `{outputFile}` completely. Read:
- `selectedSkill` from frontmatter
- `skillCategory` from frontmatter
- All context sections appended by step-02

"**Generating SKILL.md for: {selectedSkill}**

Using loaded context to build the complete skill definition."

### 2. Generate SKILL.md Content

Generate a complete SKILL.md with the following structure:

```markdown
---
name: {selectedSkill}
description: {purpose from context}
category: {core/feature/utility}
version: 1.0.0
---

# {Skill Display Name}

## Triggers

**Activation phrases and patterns:**

{Generate trigger list from context — both exact phrases and pattern descriptions}

**Trigger logic:**
- Primary triggers: {list}
- Contextual triggers: {list — phrases that activate in combination with context}

---

## Execution Flow

**Overview:** {One-sentence flow summary}

### Step-by-step flow:

{Generate numbered steps from the flow defined in context. Each step should include:}
1. **{Step name}** — {What happens}
   - Input: {what this step needs}
   - Output: {what this step produces}
   - User interaction: {what The Forge asks/tells the user}

{Continue for all flow steps}

---

## Instructions

### Role

The Forge activates this skill as: {role description for this specific skill}

### Behavior Guidelines

{Generate behavior guidelines specific to this skill:}
- How The Forge should communicate during this skill
- What level of autonomy vs collaboration
- Error handling approach
- When to ask for clarification

### Detailed Instructions

{Generate detailed step-by-step instructions that The Forge follows when executing this skill. These are the actual LLM instructions — precise, actionable, covering edge cases.}

#### Phase 1: {First phase name}

{Detailed instructions for phase 1}

#### Phase 2: {Second phase name}

{Detailed instructions for phase 2}

{Continue for all phases}

---

## Data Dependencies

**Required at runtime:**
{List files/data this skill needs access to}

**Optional enhancements:**
{List optional data that improves the skill}

---

## Connected Skills

**Leads to:** {Skills that naturally follow this one}
**Triggered by:** {Skills that naturally precede this one}
**Shares context with:** {Skills that share workspace/config context}

---

## Success Criteria

{How to know this skill executed successfully:}
- {Criterion 1}
- {Criterion 2}
- {Criterion 3}
```

### 3. Present Generated Content

"**Generated SKILL.md for {selectedSkill}. Here's the complete content:**"

{Display the full generated SKILL.md content}

"**Please review:**
- Are the triggers comprehensive and accurate?
- Does the flow match your expectations?
- Are the instructions detailed enough for The Forge to execute?
- Any missing sections or content?

**Provide feedback or confirm to write the file.**"

### 4. Process Feedback (If Any)

If user provides feedback:
- Apply requested changes
- Re-present affected sections
- Confirm changes are satisfactory

Iterate until user is satisfied.

### 5. Write SKILL.md File

Once user confirms:

"**Writing SKILL.md to: {skillOutputPath}**"

Create the directory `{forge_skills_folder}/{selectedSkill}/` if it doesn't exist.
Write the confirmed SKILL.md content to `{skillOutputPath}`.

"**SKILL.md written successfully.**"

### 6. Update Output File

Append to `{outputFile}`:

```markdown
---

## Generation Complete

**SKILL.md written to:** {skillOutputPath}
**Sections generated:** Triggers, Execution Flow, Instructions, Data Dependencies, Connected Skills, Success Criteria
**User confirmed:** Yes
```

### 7. Present MENU OPTIONS

Display: **SKILL.md generated and written. Select an option:** [C] Continue to Resource Bundling

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

#### Menu Handling Logic:

- IF C: Update {outputFile} frontmatter with stepsCompleted, then load, read entire file, then execute {nextStepFile}
- IF Any other: help user respond (edit SKILL.md if requested), then [Redisplay Menu Options](#7-present-menu-options)

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Complete SKILL.md generated with all required sections
- Triggers are comprehensive and match module brief
- Flow is detailed and step-by-step
- Instructions are actionable for an LLM
- User reviewed and confirmed content
- File written to correct path
- stepsCompleted updated

### ❌ SYSTEM FAILURE:

- Missing required SKILL.md sections
- Triggers don't match module brief descriptions
- Flow is vague or missing steps
- Instructions are too abstract for LLM execution
- Writing file without user confirmation
- Not creating skill directory

**Master Rule:** The SKILL.md must be complete, accurate, and user-confirmed before writing. Skipping steps is FORBIDDEN.
