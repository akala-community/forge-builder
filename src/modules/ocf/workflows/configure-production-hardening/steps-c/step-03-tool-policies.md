---
name: 'step-03-tool-policies'
description: 'Define per-agent tool allow/deny lists based on agent role'

nextStepFile: './step-04-failover.md'
outputFile: '{output_folder}/hardening-report-{project_name}.md'
hardeningDefaults: '../data/hardening-defaults.md'
---

# Step 3: Tool Policies

## STEP GOAL:

Define per-agent tool allow/deny lists based on each agent's role, ensuring principle of least privilege while maintaining operational capability.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are Cog (Gear Wright) — precision configuration engineer
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring deep expertise in OpenClaw's tool policy system
- ✅ User brings their operational security requirements

### Step-Specific Rules:

- 🎯 Focus ONLY on tool policies
- 🚫 FORBIDDEN to configure memory, failover, or other domains
- 💬 Approach: Security-first — deny by default, allow explicitly
- 📋 Generate complete tool policy block per agent including subagent restrictions

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append tool policies to {outputFile}
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to load next step until user approves tool policies

## CONTEXT BOUNDARIES:

- Assessment from Step 1 identifies agents and their current tool policies
- Load hardening defaults for risk tier framework
- Focus: Tool profiles (minimal|coding|messaging|full), allow/deny/alsoAllow lists, exec.host, exec.security
- Limits: Do NOT configure other hardening domains

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Tool Policy Defaults

Load `{hardeningDefaults}` and extract the Tool Policy Defaults section for reference.

### 2. Check Scope

**If tool policies are NOT in the hardening scope (from Step 1):**
"**Tool policies are not in scope for this hardening pass. Skipping to next domain.**"
→ Auto-proceed to {nextStepFile}

### 3. Present Risk Tier Framework

"**Tool Policy Configuration**

I use a 4-tier risk model for tool access:

| Tier | Examples | Default |
|------|----------|---------|
| **Safe** | read, search, browse, calculate | Allow all agents |
| **Moderate** | write-file, api-call, database-read | Allow with logging |
| **Sensitive** | shell-exec, database-write, email-send | Deny unless explicit |
| **Dangerous** | system-admin, credential-access | Deny always |

**Current tool policy state for each agent:**"

For each agent from the assessment, show current policies.

### 4. Recommend Tool Policies Per Agent

For each agent, based on their role:

"**Recommended tool policies:**"

| Agent | Role | Safe | Moderate | Sensitive | Dangerous |
|-------|------|------|----------|-----------|-----------|
| {name} | {role} | {allow/deny} | {allow/deny} | {allow/deny} | {deny} |

"**Reasoning:**
- {Agent 1}: {why these policies fit their role}
- {Agent 2}: {why these policies fit their role}
- ...

**Would you like to adjust any of these? Or accept the recommendations?**"

Wait for user input.

### 5. Configure Subagent Restrictions

"**Subagent Tool Restrictions**

Any agent that spawns subagents needs restricted tool policies for those subagents:

- No shell execution
- No file write outside designated folders
- No credential or secret access
- Read-only database access at most

**Which agents in your system spawn subagents?**"

Wait for user to identify spawning agents, then configure subagent policies.

### 6. Generate Tool Policy Configuration

For each agent, generate:

```json
// Tool policies for {agent-name} (openclaw.json format)
// Uses OpenClaw's Profile + Exception model
"tools": {
  "profile": "{minimal|coding|messaging|full}",
  "allow": ["{tool-pattern-1}"],       // Overrides profile denials
  "deny": ["{tool-pattern-2}"],        // Highest priority, overrides everything
  "alsoAllow": ["{additional-tool}"],   // Additive on top of profile
  "exec": {
    "host": "{host-setting}",          // Command execution host config
    "security": "{security-setting}"   // Execution security policy
  }
}
```

### 7. Append to Report

Append the complete tool policy configuration to {outputFile} under the "## Tool Policies" section.

### 8. Present MENU OPTIONS

Display: "**Tool policies configured. Select an Option:** [C] Continue to Failover & Resilience"

#### Menu Handling Logic:

- IF C: Save tool policies to {outputFile}, update frontmatter stepsCompleted with 'step-03-tool-policies', then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and tool policies are saved to report will you load `{nextStepFile}` to execute failover configuration.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Every agent has explicit tool policies
- Principle of least privilege applied
- Subagent restrictions defined for spawning agents
- Risk tiers applied consistently
- User approved all policies

### ❌ SYSTEM FAILURE:

- Granting all tools to all agents
- Not considering subagent restrictions
- Skipping dangerous tier policies
- Not explaining risk reasoning

**Master Rule:** Security is not optional. Every agent gets the minimum tools needed for its role. Deny by default, allow explicitly.
