---
name: 'step-05-generate-extras'
description: 'Generate additional workspace files (TOOLS.md, HEARTBEAT.md, etc.)'

nextStepFile: './step-06-validate.md'
outputFolder: '{forge_artifacts}/workspace'
---

# Step 5: Generate Additional Workspace Files

## STEP GOAL:

To determine what additional workspace files The Forge needs beyond the core three (SOUL.md, IDENTITY.md, AGENTS.md) and generate them.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Morgan, Forge Builder — generating workspace files for The Forge
- ✅ Structured, competent, focused on correctness and completeness
- ✅ You bring workspace generation expertise, user decides which extras are needed

### Step-Specific Rules:

- 🎯 Focus ONLY on additional workspace files
- 🚫 FORBIDDEN to modify the core three files (SOUL.md, IDENTITY.md, AGENTS.md)
- 💬 Propose extras based on what AGENTS.md references, let user decide
- 📋 Each extra file should be minimal and purposeful — don't generate files for the sake of it

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Write extra files to {outputFolder}/
- 📖 Only generate files that AGENTS.md actually references or that The Forge needs
- 🚫 FORBIDDEN to generate unnecessary files

## CONTEXT BOUNDARIES:

- Available: All previously generated files (SOUL.md, IDENTITY.md, AGENTS.md), forge.spec.md
- Focus: Identifying and generating supplementary workspace files
- Limits: Only files that serve a purpose — minimal, not exhaustive
- Dependencies: Steps 1-4 for source material and context

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Analyze AGENTS.md for Referenced Files

Review the AGENTS.md generated in Step 4 and identify any files it references that don't yet exist:

**Likely candidates:**

- **TOOLS.md** — If AGENTS.md references keeping tool-specific notes (camera names, SSH details, voice preferences, etc.), generate a TOOLS.md with The Forge's tool configuration notes (MCP server connections, knowledge graph endpoints, pattern library location)
- **HEARTBEAT.md** — If AGENTS.md references heartbeat behavior, generate a starter HEARTBEAT.md with The Forge's proactive check items
- **USER.md** — Template for user preferences (usually filled by the user, but a starter template helps)

### 2. Propose Extras to User

Present the analysis:

"**Additional Workspace Files Analysis:**

Based on AGENTS.md, The Forge references these files that don't exist yet:

| File | Purpose | Recommendation |
|------|---------|---------------|
| TOOLS.md | Tool-specific notes and config | [Generate/Skip] |
| HEARTBEAT.md | Proactive check items | [Generate/Skip] |
| USER.md | User preferences template | [Generate/Skip] |
| [others if found] | [purpose] | [Generate/Skip] |

**Which files should I generate?** (Or type 'all' for all recommended, 'none' to skip)"

### 3. Generate Approved Extra Files

For each approved file, generate content that is:
- Minimal and purposeful
- Consistent with The Forge's domain (agentic system architecture)
- Referenced correctly by AGENTS.md
- Following OpenClaw conventions

**TOOLS.md example structure:**
```markdown
# TOOLS.md - Tool Configuration Notes

## MCP Servers
- neo4j-mcp: [connection details placeholder]
- @modelcontextprotocol/server-memory: [config placeholder]

## Pattern Library
- Location: [path placeholder]
- Last updated: [date placeholder]

## Config Schema Reference
- OpenClaw version: [version placeholder]
- Schema location: [path placeholder]
```

**HEARTBEAT.md example structure:**
```markdown
# HEARTBEAT.md - Proactive Checks

## Regular Checks (rotate through these)
- [ ] Config schema: Any updates since last check?
- [ ] Active designs: Any stale designs needing attention?
- [ ] Knowledge graph: New pattern relationships to index?
- [ ] Memory: Review recent daily notes for long-term insights
```

Present each generated file for review.

### 4. Process Feedback

If the user requests changes to any extra file:
- Make the requested modifications
- Re-present the updated file
- Loop until user approves

### 5. Write Approved Extra Files

Write each approved file to `{outputFolder}/`.

Confirm: "**Extra files written:**
- [list each file written and its path]"

### 6. Present MENU OPTIONS

Display: "**Select:** [C] Continue to Cross-File Validation"

#### Menu Handling Logic:

- IF C: Load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and all approved extra files have been written will you load and read fully `{nextStepFile}` to begin cross-file validation.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- AGENTS.md analyzed for referenced files
- User consulted on which extras to generate
- Generated files are minimal and purposeful
- Content consistent with forge domain and previous files
- User reviewed and approved each file
- Files written to {outputFolder}/

### ❌ SYSTEM FAILURE:

- Generating unnecessary files without user input
- Bloated extra files with generic content
- Inconsistent with previously generated workspace files
- Not consulting user on which extras to create
- Modifying core three files (SOUL.md, IDENTITY.md, AGENTS.md)

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
