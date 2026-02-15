---
name: 'step-02-load-context'
description: 'Load module brief sections, patterns library, and config schema relevant to the selected skill'

nextStepFile: './step-03-generate-skill.md'
outputFile: '{forge_output_folder}/skill-build-context.md'
skillRegistryData: '../data/skill-registry.md'
moduleBriefFile: '{forge_module_brief}'
---

# Step 2: Load Skill Context

## STEP GOAL:

Load and organize all context needed to generate the selected skill's SKILL.md — module brief sections, agentic patterns library, and config schema references.

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

- 🎯 Load module brief and extract sections relevant to selected skill
- 💾 Append extracted context to {outputFile}
- 📖 Update frontmatter stepsCompleted when context loading is complete
- 🚫 FORBIDDEN to proceed without sufficient context loaded

## CONTEXT BOUNDARIES:

- Available: Selected skill from step-01 (in output file frontmatter), module brief, skill registry
- Focus: Extract only context relevant to the selected skill
- Limits: Do not generate skill content — just organize inputs
- Dependencies: step-01 must be complete (selectedSkill set)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Read Selected Skill

Load `{outputFile}` and read the `selectedSkill` from frontmatter. Confirm which skill we're building context for.

"**Loading context for skill: {selectedSkill}**"

### 2. Load Module Brief

Launch a subprocess (Pattern 3) that loads `{moduleBriefFile}` and extracts:
- The skill's row from the OpenClaw Skills tables (Core/Feature/Utility)
- The skill's trigger examples, purpose, and flow
- The agent architecture section (how The Forge operates)
- The tools & integrations section (relevant MCP tools, platform features)
- The personality and communication style section

Return only the extracted sections relevant to the selected skill.

If subprocess unavailable: Load `{moduleBriefFile}` in main thread and manually extract relevant sections.

### 3. Load Skill Registry Details

Load `{skillRegistryData}` and extract the full entry for the selected skill including:
- Detailed trigger examples
- Complete flow description
- Data needs
- Complexity assessment
- Connections to other skills

### 4. Load Agentic Patterns (If Applicable)

**If the selected skill uses agentic patterns** (design-system, recommend-pattern, setup-harness):

Extract the relevant patterns from the skill registry's Agentic Patterns Reference table. Include:
- Pattern name and when to use
- OpenClaw implementation details
- Any pattern-specific configuration

**If the skill doesn't use patterns directly:** Note this and skip.

### 5. Organize and Append Context

Append to `{outputFile}`:

```markdown
---

## Loaded Context

### Module Brief Extract

{Extracted sections from module brief relevant to this skill}

### Skill Registry Details

{Full skill entry from registry}

### Agentic Patterns (if applicable)

{Relevant patterns or "N/A — this skill does not directly implement agentic patterns"}

### Context Summary

**Key inputs for SKILL.md generation:**
- Trigger examples: {count} examples loaded
- Flow steps: {count} steps defined
- Data needs: {list}
- Related skills: {list of connected skills}
```

### 6. Present Context Summary

"**Context loaded for {selectedSkill}.**

**Loaded:**
- Module brief sections: {list what was extracted}
- Skill registry details: Complete
- Agentic patterns: {applicable/N/A}

**Key details:**
- {count} trigger examples
- {count}-step flow defined
- Data needs: {brief list}

**Anything else you'd like to add or any context I should load before we generate the SKILL.md?**"

### 7. Present MENU OPTIONS

Display: **Context loaded. Select an option:** [C] Continue to SKILL.md Generation

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

#### Menu Handling Logic:

- IF C: Update {outputFile} frontmatter with stepsCompleted, then load, read entire file, then execute {nextStepFile}
- IF Any other: help user respond (load additional context if requested), then [Redisplay Menu Options](#7-present-menu-options)

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Module brief sections extracted and organized
- Skill registry details loaded completely
- Agentic patterns loaded (if applicable)
- All context appended to output file
- User had opportunity to add additional context
- stepsCompleted updated

### ❌ SYSTEM FAILURE:

- Not loading module brief
- Missing skill registry details
- Starting to generate SKILL.md content
- Not organizing context before proceeding
- Not giving user chance to supplement context

**Master Rule:** This step gathers context only. Do not generate SKILL.md content. Skipping steps is FORBIDDEN.
