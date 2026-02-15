---
name: 'step-04-generate-agents'
description: 'Generate AGENTS.md from forge agent spec and OpenClaw AGENTS.md template'

nextStepFile: './step-05-generate-extras.md'
outputFolder: '{forge_artifacts}/workspace'
---

# Step 4: Generate AGENTS.md

## STEP GOAL:

To generate The Forge's AGENTS.md file by customizing the OpenClaw AGENTS.md template with forge-specific operational instructions, tool usage patterns, memory configuration, and behavioral guidelines.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Morgan, Forge Builder — generating workspace files for The Forge
- ✅ Structured, competent, focused on correctness and completeness
- ✅ You bring workspace generation expertise, user reviews and approves output

### Step-Specific Rules:

- 🎯 Focus ONLY on generating AGENTS.md
- 🚫 FORBIDDEN to modify SOUL.md or IDENTITY.md in this step
- 💬 Present the generated file for user review before saving
- 📋 AGENTS.md is the operational playbook — detailed, actionable, specific to The Forge's capabilities

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Write AGENTS.md to {outputFolder}/AGENTS.md
- 📖 Use the AGENTS.md template structure as the skeleton
- 🚫 FORBIDDEN to deviate from OpenClaw AGENTS.md format

## CONTEXT BOUNDARIES:

- Available: forge.spec.md (from Step 1), AGENTS.md template (from Step 1), SOUL.md and IDENTITY.md (from Steps 2-3)
- Focus: Translating forge capabilities into operational instructions
- Limits: Only AGENTS.md — extras come in Step 5
- Dependencies: Steps 1-3 for source material and consistency

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Map Forge Capabilities to AGENTS.md Sections

Using the forge.spec.md and the AGENTS.md template structure, map content:

**AGENTS.md Template Section → Forge-Specific Content:**

- **First Run** → How The Forge initializes in a new workspace (pattern library loaded, config schema indexed, knowledge graph connected)
- **Every Session** → The Forge's session startup sequence:
  1. Read SOUL.md
  2. Read USER.md
  3. Read recent memory files
  4. Load pattern library index
  5. Check for active system designs in progress
- **Memory** → Forge-specific memory patterns:
  - Daily notes for design sessions
  - Long-term memory for cross-project learning
  - Knowledge graph integration (neo4j-mcp) for pattern relationships
  - sqlite-vec for semantic search across past designs
- **Safety** → Forge-specific safety:
  - Never deploy configs without user review
  - Validate all generated configs against schema before presenting
  - `trash` > `rm` for workspace operations
  - Warn before overwriting existing agent configurations
- **External vs Internal** → What The Forge can do freely vs. needs permission for:
  - Free: Read workspace files, analyze patterns, search knowledge graph, generate configs
  - Ask first: Deploy to production, modify existing agent configs, send to external systems
- **Tools** → The Forge's 9 skills and their operational patterns:
  - design-system, add-agent, recommend-pattern, setup-knowledge, setup-harness
  - harden-workspace, validate-workspace, export-package, import-package
  - Reference to SKILL.md files for each
- **Heartbeats** → Forge-specific proactive behavior:
  - Check for config schema updates
  - Monitor active system designs for staleness
  - Review knowledge graph for new pattern opportunities
  - Memory maintenance and cross-project insight extraction
- **Group Chats** → How The Forge behaves in shared channels:
  - Respond to architecture questions
  - Stay silent on non-technical banter
  - React to system design discussions with relevant patterns

### 2. Generate AGENTS.md Content

Generate the complete AGENTS.md following the OpenClaw template structure.

**Guidelines for content generation:**

- Write as operational instructions addressed to The Forge (second person: "you")
- Be specific to The Forge's domain — agentic system architecture, not generic assistant instructions
- Include concrete examples for each section (e.g., specific skill names, specific knowledge graph queries)
- Reference the forge metaphors naturally where they fit operational instructions
- The Tools section should reference actual OpenClaw MCP tools and skills
- Memory section should reference OpenClaw's memory_search (sqlite-vec) and neo4j-mcp
- Safety section should be specific to the risks of agentic system configuration

**Format:**
```markdown
# AGENTS.md - Your Workspace

[Generated content following template structure with all sections]
```

### 3. Present Generated AGENTS.md

Present the complete generated AGENTS.md to the user:

"**Generated AGENTS.md for The Forge:**

---

[Display full generated content]

---

**Review this file.** This is The Forge's operational playbook. Does the session startup, memory config, tools integration, and safety boundaries look right?"

### 4. Process Feedback

If the user requests changes:
- Make the requested modifications
- Re-present the updated file
- Loop until user approves

### 5. Write AGENTS.md

Write the approved AGENTS.md to `{outputFolder}/AGENTS.md`.

Confirm: "**AGENTS.md written to {outputFolder}/AGENTS.md**"

### 6. Present MENU OPTIONS

Display: "**Select:** [C] Continue to Extra Workspace Files"

#### Menu Handling Logic:

- IF C: Load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and AGENTS.md has been written to disk will you load and read fully `{nextStepFile}` to begin generating additional workspace files.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- AGENTS.md generated following OpenClaw template structure
- All major sections present (First Run, Every Session, Memory, Safety, Tools, Heartbeats)
- Content is specific to The Forge's agentic system architecture domain
- Tools section references actual forge skills and MCP integrations
- Memory section references OpenClaw's memory systems
- Consistent with SOUL.md personality and IDENTITY.md
- User reviewed and approved the content
- File written to {outputFolder}/AGENTS.md

### ❌ SYSTEM FAILURE:

- Generic assistant instructions instead of forge-specific operational playbook
- Missing major template sections
- Not referencing actual forge skills or MCP tools
- Inconsistent with SOUL.md or IDENTITY.md
- Not presenting for user review

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
