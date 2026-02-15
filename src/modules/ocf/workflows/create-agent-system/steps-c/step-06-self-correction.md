---
name: 'step-06-self-correction'
description: 'Generate self-correction directives for each agent to include in their AGENTS.md'

nextStepFile: './step-07-assembly.md'
outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'
artifactSchemas: '../data/ocf-artifact-schemas.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'
---

# Step 6: Self-Correction

## STEP GOAL:

To generate self-correction directives for each agent that will be added to their AGENTS.md file. OpenClaw does not have a separate REVIEW.md file or selfCorrection config — self-correction behavior is defined as directives within AGENTS.md. These directives cover common failure modes, detection signals, recovery patterns, and error handling derived from the agent's role, capabilities, and the brief's safety/resilience requirements. This is the Quality Architect phase — designing how each agent monitors and corrects its own behavior.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- Generate content FROM the validated brief — the brief IS the user's input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with 'C', ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- You are the Quality Architect — designing how each agent monitors and corrects its own behavior
- You think about what can go wrong and build detection and recovery into each agent's design
- Self-correction is not an afterthought — it is a core capability that makes agents reliable
- You bring quality engineering expertise, user brings their understanding of acceptable failure modes

### Step-Specific Rules:

- Focus only on generating self-correction directives per agent (to be added to AGENTS.md)
- FORBIDDEN to generate assembly artifacts or modify previously generated artifacts — assembly comes in step 07
- FORBIDDEN to create a separate REVIEW.md file — OpenClaw does not use this file; self-correction goes in AGENTS.md
- Self-correction must be derived from the agent's role, capabilities, and the brief's safety/resilience requirements
- Use subprocess per agent for large rosters (Pattern 2); fallback to sequential generation

## EXECUTION PROTOCOLS:

- Follow the MANDATORY SEQUENCE exactly
- Append generated content for each agent to {outputFile} under their roster section
- Update stepsCompleted and Generation Progress table in {outputFile} frontmatter when done
- FORBIDDEN to skip any agent in the roster

## CONTEXT BOUNDARIES:

- Available: workspace-plan.md with all previous artifacts (identity, context, skills, config), source brief data
- Focus: Self-Correction — directives for AGENTS.md only
- Limits: Do NOT assemble the final directory structure, do NOT modify previous artifacts
- Dependencies: Requires all previous artifacts (identity, context, skills, config) for comprehensive self-correction design

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Context

Load {outputFile} (workspace-plan.md) and extract:
- Agent roster (names, roles, responsibilities)
- Identity artifacts (SOUL.md — principles and boundaries inform quality gates)
- Context artifacts (AGENTS.md — workspace directives will receive self-correction additions)
- Skill artifacts (SKILL.md files — skill execution informs failure modes and detection signals)
- Config artifacts (openclaw.json — error handling and resilience context)
- Architecture context (safety and resilience requirements from brief)

### 2. Generate Self-Correction Artifacts Per Agent

DO NOT BE LAZY — For EACH agent in the roster, generate self-correction artifacts:

For each agent:

a. **Analyze failure surface** — based on the agent's role and capabilities, identify:
   - What are the most likely failure modes for this specific agent?
   - What safety requirements from the brief apply to this agent?
   - What quality expectations arise from this agent's principles (SOUL.md)?
   - What skill execution errors could occur (from SKILL.md files)?

b. **Generate AGENTS.md self-correction section** to be appended to the agent's existing AGENTS.md:
   - Quality Gates: specific quality checks this agent performs on its own output
   - Common Failure Modes: failure mode paired with detection signal (how the agent knows it happened)
   - Recovery Patterns: Error Type, Detection method, Recovery Action
   - Self-Correction Directives: specific behavioral rules for error recovery (When X happens, do Y)

c. **Append generated content** to {outputFile} under the agent's roster section:
   ```markdown
   ### {Agent Display Name} — Self-Correction Directives

   #### AGENTS.md Self-Correction Section
   {generated self-correction directives to be added to AGENTS.md}
   ```

**Subprocess optimization (Pattern 2):** For agent rosters > 3 agents, launch a subprocess per agent. Each subprocess receives the agent's complete artifact set, and returns the generated self-correction directives for AGENTS.md. If subprocess unavailable, generate sequentially in main thread.

### 3. Cross-Reference Self-Correction

After all agents have self-correction artifacts:
- Verify that every agent's failure modes address their specific skills and capabilities
- Ensure recovery patterns reference valid escalation paths from AGENTS.md relationships
- Confirm that safety requirements from the brief are covered by at least one agent's quality gates
- Validate that self-correction directives don't conflict with agent boundaries (SOUL.md boundaries)
- Check that recovery paths are reflected in recovery patterns
- Fix any inconsistencies

### 4. Present Summary

"**Self-correction generation complete.**

**Agents processed:** {count}

| Agent | Quality Gates | Failure Modes | Recovery Patterns | Directives |
|-------|--------------|---------------|-------------------|------------|
| {agent-1} | {count} | {count} | {count} | {count} |
| {agent-2} | {count} | {count} | {count} | {count} |
...

**Artifacts generated per agent:** Self-correction directives for AGENTS.md (quality gates, failure modes, recovery patterns, self-correction directives)
**Safety coverage:** {count} brief safety requirements covered across agents
**Cross-references:** {verified/adjusted count} escalation and recovery paths validated"

### 5. Present MENU OPTIONS

Display: **Select an Option:** [A] Advanced Elicitation [P] Party Mode [C] Continue

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF P: Execute {partyModeWorkflow}, and when finished redisplay the menu
- IF C: Save all generated content to {outputFile}, update frontmatter stepsCompleted to include 'step-06-self-correction', update Generation Progress table (mark step 06 as Complete), then load, read entire file, then execute {nextStepFile}
- IF Any other: help user, then [Redisplay Menu Options](#5-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and all agent self-correction artifacts have been appended to {outputFile} will you then load and read fully `{nextStepFile}` to execute assembly.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Self-correction directives generated for every agent in the roster
- Directives designed to be added to each agent's AGENTS.md
- Quality gates specific to each agent's role and capabilities
- Failure modes derived from actual skills and responsibilities, not generic
- Recovery patterns reference valid escalation paths
- Self-correction directives aligned with safety requirements from brief
- Cross-references verified (escalation paths, safety coverage)
- No separate REVIEW.md created (directives go in AGENTS.md)
- All content appended to workspace-plan.md
- stepsCompleted updated

### SYSTEM FAILURE:

- Skipping any agent in the roster
- Not following self-correction directive format
- Generic failure modes not tailored to agent's specific role
- Recovery patterns referencing non-existent agents or escalation paths
- Safety requirements from brief not covered by any agent's quality gates
- Self-correction directives conflicting with agent boundaries
- Generating artifacts beyond self-correction (assembly, etc.)
- Not appending content to workspace-plan.md

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
