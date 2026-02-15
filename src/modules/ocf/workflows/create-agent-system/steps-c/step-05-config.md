---
name: 'step-05-config'
description: 'Generate openclaw.json with real config fields: model, memorySearch, tools, heartbeat, compaction, contextPruning, sandbox, subagents, groupChat, identity'

nextStepFile: './step-06-self-correction.md'
outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'
artifactSchemas: '../data/ocf-artifact-schemas.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'
---

# Step 5: Config Generation

## STEP GOAL:

To generate openclaw.json configuration per agent using the real OpenClaw config fields. Config is derived from the brief's architecture section and informed by all previous artifacts. This is the Cog (Gear Wright) phase — configuration and systems expertise.

The real openclaw.json config fields are:
- **model**: `{ primary?, fallbacks? }`
- **memorySearch**: `{ enabled?, provider? ("openai"|"local"|"gemini"|"voyage"), store? }`
- **tools**: `{ profile? ("minimal"|"coding"|"messaging"|"full"), allow?, alsoAllow?, deny?, exec?: { host?, security? }, web? }`
- **heartbeat**: `{ every?, activeHours?, model?, prompt?, target?, to? }`
- **compaction**: `{ mode? ("default"|"safeguard"), maxHistoryShare?, memoryFlush? }`
- **contextPruning**: `{ mode? ("off"|"cache-ttl"), ttl?, softTrim?, hardClear? }`
- **sandbox**: `{ mode? ("off"|"non-main"|"all"), workspaceAccess? ("none"|"ro"|"rw"), docker?, scope? }`
- **subagents**: `{ maxConcurrent?, archiveAfterMinutes?, model?, thinking? }`
- **groupChat**: `{ mentionPatterns?, historyLimit? }`
- **identity**: `{ name?, emoji?, avatar?, theme? }`

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- Generate content FROM the validated brief — the brief IS the user's input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with 'C', ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- You are Cog (Gear Wright) — configuration and systems expert
- You translate architecture decisions into concrete, deployable configuration
- Every config value must trace back to a design decision from the brief or previous artifacts
- You bring systems engineering expertise, user brings their operational requirements

### Step-Specific Rules:

- Focus on generating openclaw.json configuration per agent using real config fields
- FORBIDDEN to generate self-correction directives or assembly artifacts — those come in later steps
- FORBIDDEN to generate fabricated config files (no tool-policies.json, memory-config.json, failover-config.json, or logging-config.json — these are not real OpenClaw files)
- Config is derived from the brief's architecture section and overall design
- Follow the openclaw.json config field definitions strictly
- Use subprocess per agent for openclaw.json in large rosters (Pattern 2); fallback to sequential generation

## EXECUTION PROTOCOLS:

- Follow the MANDATORY SEQUENCE exactly
- Append generated content to {outputFile} — per-agent config under agent sections
- Update stepsCompleted and Generation Progress table in {outputFile} frontmatter when done
- FORBIDDEN to skip any agent

## CONTEXT BOUNDARIES:

- Available: workspace-plan.md with all previous artifacts (identity, context, skills), source brief data
- Focus: Configuration — openclaw.json per agent
- Limits: Do NOT generate self-correction artifacts, do NOT assemble final directory
- Dependencies: Requires all previous artifacts (identity, context, skills) for complete configuration

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Context

Load {outputFile} (workspace-plan.md) and extract:
- Agent roster (names, roles, responsibilities)
- Identity artifacts (SOUL.md, IDENTITY.md — boundaries inform permissions)
- Context artifacts (USER.md, AGENTS.md — workspace directives inform config)
- Skill artifacts (SKILL.md files — skill list informs tool settings)
- Architecture context (resilience requirements from brief)

Load {artifactSchemas} and extract the openclaw.json config field definitions.

### 2. Generate Per-Agent Config

DO NOT BE LAZY — For EACH agent in the roster, generate an openclaw.json fragment:

For each agent:

a. **Generate openclaw.json** using real config fields:
   - **model**: `{ primary?, fallbacks? }` — derived from agent's complexity and role
   - **memorySearch**: `{ enabled?, provider?, store? }` — derived from AGENTS.md memory directives
   - **tools**: `{ profile?, allow?, alsoAllow?, deny?, exec?, web? }` — derived from skill artifacts and AGENTS.md boundaries
   - **heartbeat**: `{ every?, activeHours?, model?, prompt?, target?, to? }` — if agent uses heartbeats
   - **compaction**: `{ mode?, maxHistoryShare?, memoryFlush? }` — context management strategy
   - **contextPruning**: `{ mode?, ttl?, softTrim?, hardClear? }` — context window management
   - **sandbox**: `{ mode?, workspaceAccess?, docker?, scope? }` — security boundaries from AGENTS.md
   - **subagents**: `{ maxConcurrent?, archiveAfterMinutes?, model?, thinking? }` — if agent uses subagents
   - **groupChat**: `{ mentionPatterns?, historyLimit? }` — if agent participates in group chats
   - **identity**: `{ name?, emoji?, avatar?, theme? }` — from IDENTITY.md

b. **Append generated content** to {outputFile} under the agent's roster section:
   ```markdown
   ### {Agent Display Name} — Config Artifacts

   #### openclaw.json
   ```json
   {generated openclaw.json content}
   ```
   ```

**Subprocess optimization (Pattern 2):** For agent rosters > 3 agents, launch a subprocess per agent. Each subprocess receives the agent's artifacts and config field definitions, and returns the generated openclaw.json. If subprocess unavailable, generate sequentially in main thread.

### 3. Cross-Reference Configuration

After all config is generated:
- Verify that every agent's tools config matches their skill artifacts
- Ensure memorySearch settings are consistent with AGENTS.md memory directives
- Confirm sandbox and tools settings align with AGENTS.md boundaries
- Validate that identity config matches IDENTITY.md content
- Fix any inconsistencies

### 4. Present Summary

"**Config generation complete.**

**Per-Agent Config:**

| Agent | Model | Tools Profile | Key Settings |
|-------|-------|--------------|-------------|
| {agent-1} | {model} | {profile} | {key settings summary} |
| {agent-2} | {model} | {profile} | {key settings summary} |
...

**Config fields used:** model, memorySearch, tools, heartbeat, compaction, contextPruning, sandbox, subagents, groupChat, identity (as applicable per agent)
**Cross-references:** {verified/adjusted count} config entries validated"

### 5. Present MENU OPTIONS

Display: **Select an Option:** [A] Advanced Elicitation [P] Party Mode [C] Continue

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF P: Execute {partyModeWorkflow}, and when finished redisplay the menu
- IF C: Save all generated content to {outputFile}, update frontmatter stepsCompleted to include 'step-05-config', update Generation Progress table (mark step 05 as Complete), then load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then [Redisplay Menu Options](#5-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and all per-agent openclaw.json files have been appended to {outputFile} will you then load and read fully `{nextStepFile}` to execute self-correction generation.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- openclaw.json generated for every agent in the roster using real config fields
- Config fields used correctly (model, memorySearch, tools, heartbeat, compaction, contextPruning, sandbox, subagents, groupChat, identity)
- Config values traced to brief decisions and previous artifacts
- Cross-references verified (tools match skills, memory settings consistent, sandbox aligned with boundaries)
- All content appended to workspace-plan.md
- stepsCompleted updated

### SYSTEM FAILURE:

- Skipping any agent's openclaw.json
- Using fabricated config fields not in the real OpenClaw spec
- Generating fabricated system config files (tool-policies.json, memory-config.json, failover-config.json, logging-config.json)
- Config values not traceable to design decisions
- Sandbox/tools settings not aligned with AGENTS.md boundaries
- Tools in config not matching skill artifacts
- Generating artifacts beyond config (assembly, etc.)
- Not appending content to workspace-plan.md

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
