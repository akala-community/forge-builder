---
name: 'step-05-observability'
description: 'Set up heartbeat patterns and monitoring per agent'

nextStepFile: './step-06-self-correction.md'
outputFile: '{output_folder}/hardening-report-{project_name}.md'
hardeningDefaults: '../data/hardening-defaults.md'
---

# Step 5: Observability

## STEP GOAL:

Set up heartbeat patterns per agent using OpenClaw's real heartbeat config fields (every, activeHours, model, prompt, target, to).

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
- ✅ You bring deep expertise in OpenClaw's heartbeat system
- ✅ User brings their operational monitoring requirements

### Step-Specific Rules:

- 🎯 Focus ONLY on heartbeat configuration
- 🚫 FORBIDDEN to configure memory, tools, failover, or other domains
- 💬 Approach: Operations-focused — what do you need running on a schedule?
- 📋 Generate heartbeat config per agent
- 🚫 NOTE: OpenClaw does not have a user-configurable logging block. Do not generate fabricated logging config.

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append observability configuration to {outputFile}
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to load next step until user approves observability config

## CONTEXT BOUNDARIES:

- Assessment from Step 1 identifies current observability state
- Focus: Heartbeat schedules, active hours, heartbeat prompts, target agents
- Limits: Do NOT configure other hardening domains. OpenClaw does not have user-configurable logging config.

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Observability Defaults

Load `{hardeningDefaults}` and extract the Observability Defaults section.

### 2. Check Scope

**If observability is NOT in the hardening scope:**
"**Observability is not in scope. Skipping to next domain.**"
-> Auto-proceed to {nextStepFile}

### 3. Configure Heartbeat Patterns

"**Heartbeat Configuration**

Heartbeats let agents wake up on a schedule to check in, process queued items, or monitor systems. OpenClaw injects cron-style current time into prompts.

**For each agent, I need to know:**
- Should this agent have a heartbeat? (not all agents need one)
- What frequency? (e.g., 30m, 1h, 4h -- supports ms, s, m, h units)
- What active hours? (e.g., 09:00-18:00, 24/7)
- What should the heartbeat prompt say?
- Should it target a specific agent or channel?
- What model should it use? (can differ from the agent's primary model)

**Recommended heartbeat patterns based on agent roles:**"

For each agent, recommend based on role:

| Agent | Heartbeat? | Frequency | Active Hours | Prompt |
|-------|-----------|-----------|-------------|--------|
| {name} | {yes/no} | {freq} | {hours} | {prompt pattern} |

"**Adjust any of these?**"

Wait for user input.

### 4. Generate Heartbeat Configuration

For each agent with heartbeat enabled:

```json
// Heartbeat for {agent-name} (openclaw.json format)
// Supports ms, s, m, h units. Agent reads HEARTBEAT.md and replies HEARTBEAT_OK if no action needed.
"heartbeat": {
  "every": "{frequency}",           // e.g., "30m", "1h"
  "activeHours": {
    "start": "{start}",
    "end": "{end}",
    "timezone": "{timezone}"
  },
  "model": "{model-id}",           // optional: model to use for heartbeat
  "prompt": "{heartbeat prompt}",   // what to ask the agent
  "target": "{agent-id}",          // optional: target agent
  "to": "{channel}"                // optional: target channel
}
```

### 5. Append to Report

Append heartbeat configuration to {outputFile} under "## Observability".

### 6. Present MENU OPTIONS

Display: "**Observability configured. Select an Option:** [C] Continue to Self-Correction"

#### Menu Handling Logic:

- IF C: Save observability config to {outputFile}, update frontmatter stepsCompleted with 'step-05-observability', then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and observability config is saved to report will you load `{nextStepFile}`.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Heartbeat patterns configured per agent based on role
- Active hours and timezone set appropriately
- Heartbeat model and target configured where needed
- User approved all configurations

### ❌ SYSTEM FAILURE:

- Giving all agents the same heartbeat without considering role
- Not configuring heartbeat prompts that serve a purpose

**Master Rule:** Heartbeat configuration should match each agent's operational needs. Every agent's heartbeat should serve a purpose. Not all agents need heartbeats.
