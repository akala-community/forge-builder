---
name: 'step-04-merge-config'
description: 'Merge package openclaw.json fragment into existing workspace configuration'

nextStepFile: './step-05-completion.md'
---

# Step 4: Merge Configuration

## STEP GOAL:

To read the package's `openclaw.json` configuration fragment, compare it against the user's existing `openclaw.json`, show proposed changes, merge agent entries into `agents.list[]` and bindings, and write the merged configuration with user approval.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with 'C', ensure entire file is read
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are an installation specialist (Cog / Gear Wright)
- Systematic, precise, methodical
- You bring expertise in configuration merging and conflict resolution

### Step-Specific Rules:

- Focus ONLY on merging openclaw.json configuration
- FORBIDDEN to modify workspace files (AGENTS.md, SOUL.md, etc.) - that was step 03
- Present all proposed changes to the user before writing
- Never overwrite existing config without explicit user approval
- If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- Read the package's openclaw.json fragment
- Read the user's existing openclaw.json (if present)
- Identify what will be added, changed, or merged
- Present the proposed merge for user review
- Apply the merge only after user approval
- Write the merged configuration
- DO NOT modify any workspace markdown files

## CONTEXT BOUNDARIES:

- Package's openclaw.json from the extracted archive
- User's existing openclaw.json at the target workspace or project root
- Target workspace path from step 01
- Installation results from step 03
- Dependencies: steps 01, 02, and 03 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Read Package Configuration

Read the package's `openclaw.json` from the extracted archive.

If no `openclaw.json` was included in the package:

"**No configuration fragment found in this package.** The package does not include an `openclaw.json`. No configuration merge is needed.

**Proceeding to completion...**"

Auto-proceed: Load, read entire file, then execute {nextStepFile}.

Otherwise, parse the JSON and identify the configuration sections present.

### 2. Read Existing Configuration

Look for the user's existing `openclaw.json` in these locations (in order):
1. `{target_path}/openclaw.json`
2. `{project-root}/openclaw.json`
3. `{project-root}/_bmad/openclaw.json`

**If an existing config is found:**
- Read and parse it
- Note the location for later writing

**If no existing config is found:**

"**No existing openclaw.json found.** The package configuration will be installed as a new configuration file.

**Package configuration contents:**

```json
{package_config_contents}
```

**This will be written to:** `{target_path}/openclaw.json`

**Select:** [C] Continue - install this configuration"

Wait for user input.
- IF C: Write the package config to the target path and load, read entire file, then execute {nextStepFile}
- IF Any other: help user adjust, then redisplay menu

### 3. Analyze Merge Points

Compare the package config against the existing config. Identify merge points in these categories:

**agents.list[] entries:**
- New agents to add (present in package, not in existing)
- Conflicting agents (same agent name in both, different configuration)

**bindings[] entries:**
- New bindings to add
- Conflicting bindings (same binding key, different values)

**channels configuration:**
- New channel definitions
- Conflicting channel settings

**Other top-level keys:**
- Any additional configuration keys in the package not present in existing

### 4. Present Merge Plan

"**Configuration Merge Plan**

---

**Existing config:** `{existing_config_path}`
**Package config:** from `{system_name}.ocf.zip`

### Additions (will be added):

**New agents:**
{list each new agent entry with its configuration}

**New bindings:**
{list each new binding entry}

**New channels:**
{list each new channel definition, or 'None'}

### Conflicts (need resolution):

{for each conflict:}
**`{key}`:**
- Existing: `{existing_value}`
- Package: `{package_value}`
- Recommendation: {keep existing / use package / merge both}

### Unchanged (no action needed):

{list sections that exist in both but are identical, or 'None'}

---"

### 5. Resolve Conflicts

If conflicts were detected, present resolution options for each:

"**Conflict Resolution**

For each conflict below, select how to resolve it:

**{conflict_key}:**
- [E] Keep existing value
- [P] Use package value
- [M] Manually specify a value

**Select for `{conflict_key}`:**"

Wait for user input on each conflict. Record the resolution.

If no conflicts were detected, skip this section.

### 6. Show Merged Result

Build the merged configuration by:
1. Starting with the existing config as the base
2. Adding all new agent entries to `agents.list[]`
3. Adding all new bindings to `bindings[]`
4. Adding any new channel definitions
5. Applying conflict resolutions from section 5
6. Adding any other new top-level keys

Present the complete merged result:

"**Merged Configuration Preview**

```json
{merged_config_json}
```

**Changes summary:**
- {count} agent(s) added
- {count} binding(s) added
- {count} conflict(s) resolved
- {count} other key(s) added

**Select:** [C] Continue - write this configuration | [E] Edit before writing"

Wait for user input.

### 7. Write Merged Configuration

- IF C: Write the merged config to the existing config location (or `{target_path}/openclaw.json` if new)
- IF E: Allow user to specify changes, rebuild, re-present, then write when approved

"**Configuration written to:** `{config_path}`"

Auto-proceed: Load, read entire file, then execute {nextStepFile}.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Package openclaw.json read and parsed
- Existing openclaw.json located and parsed (or absence noted)
- Merge points identified across all config sections
- Proposed changes presented clearly to user
- Conflicts resolved with user input
- Merged result previewed and approved
- Merged config written to correct location
- No data loss from existing config

### FAILURE:

- Overwriting existing config without merge
- Not showing the user what will change
- Silently dropping existing config entries
- Not handling conflicts with user input
- Writing config without user approval
- Modifying workspace markdown files in this step

**Master Rule:** Merge configuration safely with full transparency. Show every proposed change. Never lose existing configuration data. Write ONLY after user approval.
