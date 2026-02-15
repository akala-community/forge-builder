---
name: 'step-02-load-context'
description: 'Load forge agent specs, existing skills, and module brief for context'

nextStepFile: './step-03-generate-spec.md'
outputFile: '{forge_artifacts}/add-skill-context.md'
forgeSpecFile: '{project-root}/src/modules/forge/agents/forge.spec.md'
forgeBuilderSpecFile: '{project-root}/src/modules/forge/agents/forge-builder.spec.md'
moduleBriefFile: '{forge_module_brief}'
existingSkillsFolder: '{project-root}/_bmad/forge/skills'
---

# Step 2: Load Module Context

## STEP GOAL:

Load and organize all module context needed to generate the new skill's SKILL.md — agent specifications, existing skill definitions, and module brief.

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
- ✅ Professional, precise, focused on gathering the right context
- ✅ You bring expertise in what information a skill definition needs
- ✅ User can provide additional context or corrections

### Step-Specific Rules:

- 🎯 Focus ONLY on loading and organizing context — no SKILL.md generation
- 🚫 FORBIDDEN to start writing the SKILL.md
- 💬 Use subprocess Pattern 3 to load large data files and extract relevant sections
- ⚙️ If subprocess unavailable, load and scan files in main thread

## EXECUTION PROTOCOLS:

- 🎯 Load agent specs and existing skills to understand the landscape
- 💾 Append extracted context to {outputFile}
- 📖 Update frontmatter stepsCompleted when context loading is complete
- 🚫 FORBIDDEN to proceed without sufficient context loaded

## CONTEXT BOUNDARIES:

- Available: Skill concept from step-01 (in output file), module files
- Focus: Extract context relevant to skill generation and conflict detection
- Limits: Do not generate skill content — just organize inputs
- Dependencies: step-01 must be complete (skill concept defined)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Read Skill Concept

Load `{outputFile}` and read the skill concept from step-01.

"**Loading context for new skill: {skillName}**"

### 2. Load The Forge Agent Spec

Launch a subprocess (Pattern 3) that loads `{forgeSpecFile}` and extracts:
- The Forge's current command table (planned commands)
- Agent persona and communication style
- Shared context and workflow references

If subprocess unavailable: Load `{forgeSpecFile}` in main thread and extract relevant sections.

### 3. Load Forge Builder Spec

Launch a subprocess (Pattern 3) that loads `{forgeBuilderSpecFile}` and extracts:
- Morgan's current command table (this is where the new skill will be registered)
- Existing trigger/command mappings
- Build pipeline structure

If subprocess unavailable: Load `{forgeBuilderSpecFile}` in main thread and extract relevant sections.

### 4. Scan Existing Skills

List all existing skills in `{existingSkillsFolder}`:

For each skill directory found:
- Read the SKILL.md if it exists
- Extract: name, triggers, category, connected skills
- Note any potential conflicts with the new skill

"**Existing skills found:** {count}
**Skills:** {list with categories}"

If no skills directory or no skills found:
"**No existing skills found.** This will be the first skill built for The Forge."

### 5. Load Module Brief (If Available)

If `{moduleBriefFile}` exists:

Launch a subprocess (Pattern 3) that loads the module brief and extracts:
- Skill-related sections
- Architecture guidance
- Any references to the new skill's domain

If unavailable: Note that module brief was not found and proceed.

### 6. Organize and Append Context

Append to `{outputFile}`:

```markdown
---

## Loaded Context

### The Forge Agent Spec

**Current Commands:**
{command table extract}

**Communication Style:**
{style summary}

### Forge Builder Spec

**Current Build Commands:**
{command table extract}

**Existing Trigger Mappings:**
{trigger/command list}

### Existing Skills

**Count:** {count}
**Skills:**
{list with name, category, triggers for each}

### Module Brief Extract

{relevant sections or 'Not available'}

### Context Summary

**Key inputs for SKILL.md generation:**
- Existing commands: {count} in The Forge, {count} in Forge Builder
- Existing skills: {count} built
- Potential trigger conflicts: {list or 'None detected'}
- Available trigger letter: {suggest unused 2-letter trigger}
```

### 7. Present Context Summary

"**Context loaded for {skillName}.**

**Loaded:**
- The Forge agent spec: {summary}
- Forge Builder spec: {summary}
- Existing skills: {count} found
- Module brief: {available/not available}

**Potential conflicts detected:** {list or 'None'}
**Suggested trigger code:** {2-letter code}

**Anything else you'd like me to load before we generate the SKILL.md?**"

### 8. Present MENU OPTIONS

Display: **Context loaded. Select an option:** [C] Continue to Spec Generation

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

#### Menu Handling Logic:

- IF C: Update {outputFile} frontmatter with stepsCompleted, then load, read entire file, then execute {nextStepFile}
- IF Any other: help user respond (load additional context if requested), then [Redisplay Menu Options](#8-present-menu-options)

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- The Forge agent spec loaded and command table extracted
- Forge Builder spec loaded and command table extracted
- Existing skills scanned for conflict detection
- Module brief loaded (if available)
- All context appended to output file
- Potential conflicts identified
- Trigger code suggested
- stepsCompleted updated

### ❌ SYSTEM FAILURE:

- Not loading agent specs
- Skipping existing skills scan
- Starting to generate SKILL.md content
- Not identifying potential conflicts
- Not giving user chance to add context

**Master Rule:** This step gathers context only. Do not generate SKILL.md content. Skipping steps is FORBIDDEN.
