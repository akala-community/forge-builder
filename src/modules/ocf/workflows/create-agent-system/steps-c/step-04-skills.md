---
name: 'step-04-skills'
description: 'Generate skills/ directory structure and SKILL.md files for each agent'

nextStepFile: './step-05-config.md'
outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'
artifactSchemas: '../data/ocf-artifact-schemas.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'
---

# Step 4: Skill Generation

## STEP GOAL:

To generate the skills/ directory structure and SKILL.md files for each agent — mapping capabilities to concrete, invocable skills. Each skill is derived from the brief's Skill & Channel Mapping section and informed by the agent's identity and context from steps 02-03. This is the Skill Architect phase.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- Generate content FROM the validated brief — the brief IS the user's input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with 'C', ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- You are the Skill Architect — mapping capabilities to concrete, invocable skills
- You translate abstract responsibilities into well-defined, triggerable skill definitions
- Each skill should have clear invocation triggers, gating rules, and output formats
- You bring skill architecture expertise, user brings their requirements for agent capabilities

### Step-Specific Rules:

- Focus only on generating SKILL.md files and skills/ directory structure per agent
- FORBIDDEN to generate config files, REVIEW.md, or assembly artifacts — those come in later steps
- Skills are derived from the brief's Skill & Channel Mapping section
- Use subprocess per agent for large rosters (Pattern 2); fallback to sequential generation
- Follow the SKILL.md schema from {artifactSchemas} strictly

## EXECUTION PROTOCOLS:

- Follow the MANDATORY SEQUENCE exactly
- Append generated content for each agent to {outputFile} under their roster section
- Update stepsCompleted and Generation Progress table in {outputFile} frontmatter when done
- FORBIDDEN to skip any agent in the roster

## CONTEXT BOUNDARIES:

- Available: workspace-plan.md with agent roster, identity artifacts (step 02), context artifacts (step 03)
- Focus: Skills — SKILL.md files and skills/ directory structure only
- Limits: Do NOT generate config, self-correction, or assembly artifacts
- Dependencies: Requires completed steps 02-03 (identity and context inform skill design)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Context

Load {outputFile} (workspace-plan.md) and extract:
- Agent roster (names, roles, responsibilities)
- Skill & Channel Mapping data from the source brief
- Identity artifacts (SOUL.md, IDENTITY.md — capabilities inform skill definitions)
- Context artifacts (USER.md, AGENTS.md — user context and workspace directives inform skill parameters)

Load {artifactSchemas} and extract the SKILL.md schema.

### 2. Generate Skill Artifacts Per Agent

DO NOT BE LAZY — For EACH agent in the roster, generate skill artifacts:

For each agent:

a. **Identify skills from the brief** — extract from the Skill & Channel Mapping section:
   - What skills were assigned to this agent?
   - What channels were bound to this agent?
   - What shared vs. unique skills apply?

b. **Generate SKILL.md files** — for each skill assigned to this agent, following the schema:
   - Frontmatter with `name` (kebab-case identifier) and `description` (comprehensive description that serves as the primary trigger mechanism — tells the agent when and why to use this skill)
   - Body content with instructions for the agent on HOW to use the skill (concise, imperative form, under 500 lines)

c. **Define skills/ directory structure** for this agent:
   ```
   {agent-name}/
     skills/
       {skill-1-name}.md
       {skill-2-name}.md
       ...
   ```

d. **Append generated content** to {outputFile} under the agent's roster section:
   ```markdown
   ### {Agent Display Name} — Skill Artifacts

   #### Skills Directory: {agent-name}/skills/

   ##### {skill-1-name}.md
   {generated SKILL.md content}

   ##### {skill-2-name}.md
   {generated SKILL.md content}
   ```

**Subprocess optimization (Pattern 2):** For agent rosters > 3 agents, launch a subprocess per agent. Each subprocess receives the agent's brief data, identity/context artifacts, and skill schema, and returns the generated SKILL.md files. If subprocess unavailable, generate sequentially in main thread.

### 3. Cross-Reference Skills

After all agents have skill artifacts:
- Verify that shared skills are defined consistently across agents that use them
- Confirm every capability listed in AGENTS.md has a corresponding skill definition
- Ensure skill descriptions are comprehensive enough to serve as the trigger mechanism
- Identify any gaps — capabilities without skills or skills without a clear capability source
- Fix any inconsistencies

### 4. Present Summary

"**Skill generation complete.**

**Agents processed:** {count}

| Agent | Skills Count | Shared Skills |
|-------|-------------|---------------|
| {agent-1} | {count} | {shared skill list} |
| {agent-2} | {count} | {shared skill list} |
...

**Total skills generated:** {total count}
**Shared skills:** {list of skills used by multiple agents}"

### 5. Present MENU OPTIONS

Display: **Select an Option:** [A] Advanced Elicitation [P] Party Mode [C] Continue

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF P: Execute {partyModeWorkflow}, and when finished redisplay the menu
- IF C: Save all generated content to {outputFile}, update frontmatter stepsCompleted to include 'step-04-skills', update Generation Progress table (mark step 04 as Complete), then load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then [Redisplay Menu Options](#5-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and all agent skill artifacts have been appended to {outputFile} will you then load and read fully `{nextStepFile}` to execute config generation.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- SKILL.md files generated for every skill assigned to every agent
- Skills/ directory structure defined for each agent
- Frontmatter uses correct fields (name + description only)
- Skills derived from brief's Skill & Channel Mapping section
- Descriptions comprehensive enough to serve as trigger mechanism
- Shared vs. unique skills properly handled
- Every AGENTS.md capability has a corresponding skill
- All content appended to workspace-plan.md
- stepsCompleted updated

### SYSTEM FAILURE:

- Skipping any agent in the roster
- Not following SKILL.md frontmatter format (name + description)
- Skills not tied to brief's Skill & Channel Mapping
- Descriptions that don't include trigger information
- Capabilities in AGENTS.md without corresponding skills
- Generating artifacts beyond skills (config, REVIEW.md, etc.)
- Not appending content to workspace-plan.md

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
