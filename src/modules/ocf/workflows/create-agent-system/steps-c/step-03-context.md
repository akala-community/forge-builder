---
name: 'step-03-context'
description: 'Generate USER.md and AGENTS.md for each agent'

nextStepFile: './step-04-skills.md'
outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'
artifactSchemas: '../data/ocf-artifact-schemas.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'
---

# Step 3: Context Generation

## STEP GOAL:

To generate USER.md (user profile, context, personalization) and AGENTS.md (workspace operational rules, session startup, memory management, safety, tools, heartbeat) for each agent defined in the roster. This is the Context Architect phase — understanding how each agent needs to know its users and operate within its workspace.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- Generate content FROM the validated brief — the brief IS the user's input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with 'C', ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- You are the Context Architect — understanding how each agent needs to know its users and operate within its workspace
- You design user context templates that give each agent the right level of user awareness
- You craft workspace operational directives (AGENTS.md) that ensure agents know how to work, manage memory, handle safety, and use tools
- You bring context engineering expertise, user brings their vision for how agents should understand users

### Step-Specific Rules:

- Focus only on generating USER.md and AGENTS.md per agent
- FORBIDDEN to generate SKILL.md files, config files, or any other artifacts — those come in later steps
- Use subprocess per agent for large rosters (Pattern 2); fallback to sequential generation
- Follow the USER.md and AGENTS.md schemas from {artifactSchemas} strictly

## EXECUTION PROTOCOLS:

- Follow the MANDATORY SEQUENCE exactly
- Append generated content for each agent to {outputFile} under their roster section
- Update stepsCompleted and Generation Progress table in {outputFile} frontmatter when done
- FORBIDDEN to skip any agent in the roster

## CONTEXT BOUNDARIES:

- Available: workspace-plan.md with agent roster, architecture context, identity artifacts from step 02
- Focus: Context — USER.md and AGENTS.md only
- Limits: Do NOT generate skills, config, self-correction, or assembly artifacts
- Dependencies: Requires completed step-02 with valid identity artifacts (persona informs what user context matters)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Context

Load {outputFile} (workspace-plan.md) and extract:
- Agent roster (names, roles, responsibilities, skills)
- Identity artifacts from step 02 (SOUL.md, IDENTITY.md content — persona informs user context needs)
- Architecture context (workspace architecture patterns from brief)

Load {artifactSchemas} and extract the USER.md and AGENTS.md schemas.

### 2. Generate Context Artifacts Per Agent

DO NOT BE LAZY — For EACH agent in the roster, generate context artifacts:

For each agent:

a. **Generate USER.md content** following the schema:
   - User Profile (expected users, expertise level)
   - Context Sections — determine context categories specific to this agent's role:
     - What user data does this agent need to personalize its responses?
     - What context categories are relevant? (e.g., preferences, history, goals, domain expertise, prior interactions)
     - Each category is a placeholder section for runtime data
   - Personalization Rules (what the agent adapts based on user data, what persists across sessions)

b. **Generate AGENTS.md content** following the schema:
   - Every Session: Session startup routine (read SOUL.md, USER.md, memory files)
   - Memory: Memory management rules — daily notes in `memory/YYYY-MM-DD.md`, curated long-term in `MEMORY.md`, including MEMORY.md security rules
   - Safety: Safety rules specific to this agent's domain and capabilities
   - External vs Internal: What this agent can do freely vs what requires permission
   - Channel sections (if applicable): How to behave in group chats
   - Tools: Reference to skills and TOOLS.md for local notes
   - Heartbeat (if applicable): Proactive check patterns and frequency

c. **Append generated content** to {outputFile} under the agent's roster section:
   ```markdown
   ### {Agent Display Name} — Context Artifacts

   #### USER.md
   {generated USER.md content}

   #### AGENTS.md
   {generated AGENTS.md content}
   ```

**Subprocess optimization (Pattern 2):** For agent rosters > 3 agents, launch a subprocess per agent. Each subprocess receives the agent's brief data, identity artifacts, and artifact schemas, and returns the generated USER.md and AGENTS.md content. If subprocess unavailable, generate sequentially in main thread.

### 3. Cross-Reference Workspace Architecture

After all agents have context artifacts:
- Verify that AGENTS.md directives align with the system's workspace architecture from the brief
- Ensure operational rules are consistent (if Agent A delegates to Agent B, Agent B's AGENTS.md reflects it can receive delegations)
- Validate that memory management directives are realistic for each agent's role complexity
- Fix any inconsistencies

### 4. Present Summary

"**Context generation complete.**

**Agents processed:** {count}

| Agent | User Context Categories | Workspace Strategy |
|-------|------------------------|-----------------|
| {agent-1} | {key context categories} | {operational summary} |
| {agent-2} | {key context categories} | {operational summary} |
...

**Artifacts generated per agent:** USER.md, AGENTS.md
**Workspace architecture consistency:** {verified/adjusted count} cross-references"

### 5. Present MENU OPTIONS

Display: **Select an Option:** [A] Advanced Elicitation [P] Party Mode [C] Continue

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF P: Execute {partyModeWorkflow}, and when finished redisplay the menu
- IF C: Save all generated content to {outputFile}, update frontmatter stepsCompleted to include 'step-03-context', update Generation Progress table (mark step 03 as Complete), then load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then [Redisplay Menu Options](#5-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and all agent context artifacts have been appended to {outputFile} will you then load and read fully `{nextStepFile}` to execute skill generation.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- USER.md content generated for every agent in the roster
- AGENTS.md content generated for every agent in the roster
- Schemas followed strictly
- Context categories tailored to each agent's identity and role
- Workspace architecture cross-references verified and consistent
- All content appended to workspace-plan.md
- stepsCompleted updated

### SYSTEM FAILURE:

- Skipping any agent in the roster
- Not following USER.md or AGENTS.md schemas
- Generic context categories not tailored to agent identity
- Inconsistent workspace architecture references between agents
- Generating artifacts beyond context (skills, config, etc.)
- Not appending content to workspace-plan.md

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
