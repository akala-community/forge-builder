---
name: 'step-06-policies'
description: 'Define subagent tool restrictions, sandbox policies, and per-agent capability boundaries'

nextStepFile: './step-07-assembly.md'
outputFile: '{ocf_output_folder}/orchestration-design-{project_name}.md'
toolPolicyReference: '../data/tool-policy-reference.md'
orchestrationReference: '../data/openclaw-orchestration-reference.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
---

# Step 6: Subagent Policies

**Progress: Step 6 of 7** — Next: Assembly

## STEP GOAL:

Define tool restrictions for spawned subagents, per-agent sandbox configuration, and capability boundaries that ensure each agent has exactly the tools it needs -- no more, no less. Uses OpenClaw's real tool config: profile (minimal|coding|messaging|full), allow, alsoAllow, deny, and exec (host, security).

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a systems architect designing security boundaries
- ✅ If you already have been given a name, communication_style and persona, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring expertise in least-privilege design — reference {toolPolicyReference} and {orchestrationReference} for tool policy and sandbox syntax

### Step-Specific Rules:

- 🎯 Focus only on tool restrictions and sandbox policies
- 🚫 FORBIDDEN to redesign communication patterns or bindings
- 💬 Approach: For each agent, determine appropriate capability boundaries
- 📋 Use {toolPolicyReference} for default denied tools, config syntax, and sandbox options

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append the Subagent Policies section to {outputFile} when complete
- 📖 Update frontmatter stepsCompleted to add this step when completed
- 🚫 FORBIDDEN to load next step until user selects 'C'

## CONTEXT BOUNDARIES:

- Available context: Agent Map (Step 2), Communication Patterns (Step 3), Failure Handling (Step 5)
- Focus: Tool restrictions, sandbox config, capability boundaries
- Limits: Don't redesign communication or binding patterns
- Dependencies: Agent roles from Step 2, spawn relationships from Step 3

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Explain Default Sub-Agent Tool Policy

Using {toolPolicyReference}, present the default denied tools table and explain what sub-agents CAN do by default. Ask if additional restrictions are needed.

### 2. Design Per-Agent Tool Policies

For each agent in the roster, collaboratively determine: what tool profile to use (minimal|coding|messaging|full), what additional tools to allow or deny, and exec settings (host, security). Reference {toolPolicyReference} for config syntax. Ask 1-2 questions per agent.

```json
// Tool policy for {agent-id} (openclaw.json format)
"tools": {
  "profile": "{minimal|coding|messaging|full}",
  "allow": ["{tool-pattern}"],
  "alsoAllow": ["{additional-tool}"],
  "deny": ["{denied-tool}"],
  "exec": {
    "host": "{host-setting}",
    "security": "{security-setting}"
  }
}
```

### 3. Design Sub-Agent Tool Overrides

Discuss whether sub-agents should have additional global restrictions beyond the defaults (e.g., deny `browser`, deny `write`/`edit`). Reference {toolPolicyReference} for override syntax.

### 4. Design Sandbox Configuration

For each agent, determine: sandbox mode (off|non-main|all), workspaceAccess (none|ro|rw), docker setting, and scope. Reference {toolPolicyReference} for sandbox config syntax.

```json
// Sandbox for {agent-id} (openclaw.json format)
"sandbox": {
  "mode": "{off|non-main|all}",
  "workspaceAccess": "{none|ro|rw}",
  "docker": {true/false},
  "scope": "{scope-setting}"
}
```

### 5. Design Sub-Agent Model Defaults

Configure default sub-agent model, thinking level, and concurrency limits using the real subagents config. Discuss per-agent overrides where needed. Reference {toolPolicyReference} for model config syntax.

```json
// Subagent defaults (openclaw.json format)
"subagents": {
  "maxConcurrent": {number},
  "archiveAfterMinutes": {number},
  "model": "{model-id}",
  "thinking": "{thinking-level}"
}
```

### 6. Assemble Subagent Policies Section

Compile into the output document section with: per-agent tool configuration table, global sub-agent tool overrides, sandbox configuration table, sub-agent model configuration, and capability summary.

Present for review: "Is any agent too permissive? Too restrictive? Does least-privilege feel right?"

### 7. Present MENU OPTIONS

Display: "**Select an Option:** [A] Advanced Elicitation [C] Continue"

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF C: Append Subagent Policies section to {outputFile}, update frontmatter (add 'step-06-policies' to stepsCompleted), then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#7-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [C continue option] is selected and [Subagent Policies section appended to output file with frontmatter updated], will you then load and read fully `{nextStepFile}` to begin final assembly.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Every agent has defined tool policies (even if "default")
- Sub-agent tool overrides are documented
- Sandbox configuration is specified per agent
- Sub-agent model defaults are configured
- Capability summary is clear and follows least-privilege
- User has verified security boundaries

### ❌ SYSTEM FAILURE:

- Agents without defined tool policies
- Not addressing sandbox configuration
- Overly permissive defaults without justification
- Not configuring sub-agent model defaults

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
