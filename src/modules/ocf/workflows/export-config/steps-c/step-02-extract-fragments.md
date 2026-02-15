---
name: 'step-02-extract-fragments'
description: 'Extract all openclaw.json-relevant configuration from workspace artifacts'

nextStepFile: './step-03-format-complete.md'
outputFile: '{output_folder}/openclaw-config-{project_name}.md'
configDomains: '../data/config-domains.md'
---

# Step 2: Extract Fragments

## STEP GOAL:

Extract all openclaw.json-relevant configuration from the workspace artifacts inventoried in Step 1, generating properly structured JSON fragments for each configuration domain.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are Cog (Gear Wright) — precision configuration engineer
- ✅ If you already have been given communication or persona patterns, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring deep expertise in OpenClaw's openclaw.json schema
- ✅ User brings their workspace context and deployment requirements

### Step-Specific Rules:

- 🎯 Focus ONLY on extracting configuration fragments from workspace artifacts
- 🚫 FORBIDDEN to format for merge or generate merge instructions — that happens in Step 3
- 💬 Approach: Systematic extraction — domain by domain, agent by agent
- 📋 Generate valid JSON fragments that conform to OpenClaw's Zod schema
- 🔧 When workspace artifacts are ambiguous, present options and ask user to clarify

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append extracted fragments to {outputFile} under the appropriate sections
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to skip any domain that has data (from Step 1 inventory)

## CONTEXT BOUNDARIES:

- Step 1 inventory identifies which domains have data
- Load {configDomains} for extraction mapping and JSON schema reference
- Focus: Extract JSON fragments from workspace artifacts
- Limits: Do NOT format for merge — just extract raw fragments
- Dependencies: Step 1 inventory and workspace files

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Extraction Reference

Load `{configDomains}` to understand the mapping from workspace artifacts to openclaw.json structure. Use the JSON schema examples in each domain section as the target output format.

Load `{outputFile}` to review the inventory from Step 1.

### 2. Extract Agent Entries

"**Extracting agent entries...**"

From AGENTS.md, SOUL.md, and agent.yaml (where present), construct agent entries matching the schema in {configDomains} § Agent Entries.

**For each agent, derive:**
- `id`: from agent filename, folder name, or explicit ID in config
- `name`: from SOUL.md persona name or AGENTS.md header
- `workspace`: the agent's working directory (ask user if unclear)
- `model`: from agent config, or mark as `"[SET_MODEL]"` if not specified
- `identity`: from SOUL.md persona section

Present the extracted agent entries for user review:

"**Agent entries extracted:**

{Show JSON for each agent}

**Do these look correct? Any adjustments needed?**"

Wait for user confirmation or adjustments.

### 3. Extract Bindings

"**Extracting channel bindings...**"

From channel configurations, AGENTS.md channel mentions, and orchestration patterns, construct binding entries matching the schema in {configDomains} § Bindings.

**Extraction logic:**
- Each agent-channel mention in AGENTS.md = potential binding
- If channel IDs are present, include them
- If only channel types are specified, use placeholder IDs with `[SET_ID]` markers
- Multiple channels per agent = multiple binding entries

Present bindings for review. If no binding data exists, note it:

"**No explicit binding data found in workspace. You'll need to configure bindings manually based on your deployment channels.**"

### 4. Extract Tool Policies

"**Extracting tool policies...**"

For each agent with tool policy information, extract entries matching the schema in {configDomains} § Tool Policies.

**Extraction logic:**
- Map agent role descriptions to appropriate profiles
- Extract explicit allow/deny lists from AGENTS.md directives
- Note subagent restrictions for spawning agents
- If no explicit policy exists, recommend based on agent role

Present per-agent tool policies for review.

### 5. Extract Memory Configuration

"**Extracting memory configuration...**"

From MEMORY.md, _memory/ folders, and AGENTS.md memory directives, construct config matching {configDomains} § Memory Configuration.

**Extraction logic:**
- Presence of MEMORY.md = memory enabled
- Presence of _memory/{agent}/ sidecar = agent has dedicated memory
- Memory directives in AGENTS.md indicate recall/capture preferences
- If no memory artifacts exist, set backend to disabled

Present memory config for review.

### 6. Extract Model / Failover

"**Extracting model and failover configuration...**"

From agent configurations and failover specifications, construct config matching {configDomains} § Model / Failover.

**Extraction logic:**
- If agent has explicit model assignment, use it
- If failover chain specified, include fallbacks array
- If no model specified, mark as `"[SET_MODEL]"` placeholder
- Default agents can use `agents.defaults.model`

Present model configs for review.

### 7. Extract Heartbeat

"**Extracting heartbeat configuration...**"

From HEARTBEAT.md and heartbeat directives, construct config matching {configDomains} § Heartbeat.

**Extraction logic:**
- HEARTBEAT.md content → heartbeat prompt
- Active hours from agent config or workspace defaults
- Frequency from heartbeat directives
- If no heartbeat artifacts, skip this domain

Present heartbeat configs for review.

### 8. Extract Logging

"**Extracting logging configuration...**"

From workspace logging settings and observability configurations, construct config matching {configDomains} § Logging.

**Extraction logic:**
- Logging level from workspace config or environment target
- Redaction settings from security/privacy configurations
- Console style based on deployment target (pretty for dev, json for prod)
- If no logging config exists, provide sensible defaults

Present logging config for review.

### 9. Append All Fragments to Report

Append the extracted fragments to {outputFile}:

- Agent entries → **Agent Configuration Fragments** section
- Bindings → **Bindings Configuration** section
- Tool policies, memory, model, heartbeat, logging → **System Configuration Fragments** section

Each fragment should include a brief label identifying the domain and agent it belongs to.

### 10. Present Extraction Summary

"**Extraction complete.**

**Fragments extracted:**

| Domain | Entries | Status |
|--------|---------|--------|
| Agent Entries | {count} | ✅ Extracted |
| Bindings | {count} | ✅ Extracted / ⚠️ Placeholder IDs |
| Tool Policies | {count} agents | ✅ Extracted |
| Memory | {global + overrides} | ✅ Extracted |
| Model / Failover | {count} agents | ✅ Extracted |
| Heartbeat | {count} agents | ✅ Extracted / ⏭️ Skipped |
| Logging | {system-wide} | ✅ Extracted |

**Placeholders requiring manual configuration:** {list any [SET_*] markers}

Next step: I'll format everything for clean merge into your openclaw.json."

### 11. Present MENU OPTIONS

Display: "**Extraction complete. Select an Option:** [C] Continue to Format & Complete"

#### Menu Handling Logic:

- IF C: Save fragments to {outputFile}, update frontmatter stepsCompleted with 'step-02-extract-fragments', then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- User can chat or ask questions — always respond and redisplay menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and all fragments are saved to the output document will you load and read fully `{nextStepFile}` to execute formatting and completion.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All 7 configuration domains processed
- Valid JSON fragments generated for each domain with data
- Fragments conform to OpenClaw's Zod schema structure
- User reviewed and approved each domain's extraction
- All fragments appended to output document
- Placeholder markers used for unknown values (not guessed)

### ❌ SYSTEM FAILURE:

- Skipping domains that have data in the inventory
- Generating invalid JSON structure
- Not conforming to openclaw.json schema
- Guessing values instead of using placeholders
- Not presenting fragments for user review
- Missing agents from extraction

**Master Rule:** Extract systematically, domain by domain. Every fragment must be valid JSON conforming to the openclaw.json schema. Use placeholder markers for unknown values — never guess.
