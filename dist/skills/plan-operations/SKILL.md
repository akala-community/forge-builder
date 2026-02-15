---
name: plan-operations
description: Analyze a completed agent system and recommend execution modes (manual, cron/heartbeat, webhook, human-in-the-loop) for each agent/workflow, then collaboratively implement the operational config
category: core
version: 1.0.0
---

# Plan Operations

## Triggers

**Activation phrases and patterns:**

- "plan my operations"
- "plan operations"
- "set up automation schedules"
- "how should I run my agents"
- "configure cron jobs for my team"
- "operationalize my system"
- "set up cron"
- "schedule my agents"
- "automate my workflows"
- "what should run automatically"

**Trigger logic:**
- Primary triggers: "plan operations", "set up automation", "how should I run my agents"
- Contextual triggers: "what should run on a schedule?", "which agents need webhooks?", "should anything run automatically?" — activate when workspace is fully set up (agents defined, equipped, hardened) and the user wants to move to operational readiness

---

## Execution Flow

**Overview:** Analyze the user's completed agent system, classify each agent's ideal execution mode(s), propose an operations plan, iterate with the user, implement the automation config into openclaw.json, and validate consistency.

### Step-by-step flow:

1. **Load and Analyze System** — Read the full workspace to understand what's been built
   - Input: User's workspace directory (openclaw.json, agent workspace files, bindings, existing cron/hooks/heartbeat config)
   - Output: Complete inventory of agents, their roles, interaction patterns, and current automation state
   - User interaction: "Let me read your system and understand what we're working with — agents, roles, how they connect."

2. **Classify Execution Modes** — For each agent/workflow, determine the right execution mode(s)
   - Input: Agent inventory, roles, interdependencies, agentic pattern in use
   - Output: Per-agent execution mode recommendation with rationale
   - User interaction: Present a classification table showing each agent and its recommended mode(s) with reasoning. Ask user to review and adjust.

3. **Propose Operations Plan** — Build a structured operational plan
   - Input: Confirmed execution mode classifications
   - Output: Complete operations plan with cron schedules, heartbeat intervals, webhook mappings, approval workflows, and channel routing
   - User interaction: Present the full plan in a structured format. Walk through each section: "Here's the schedule I'd set for your monitor agent — every 15 minutes during business hours. Here's the webhook mapping for your PR reviewer. Here's the approval flow for your deployment agent."

4. **User Review and Refinement** — Collaborative iteration
   - Input: User feedback on proposed plan
   - Output: Refined operations plan
   - User interaction: Iterate on specific items — adjust schedules, change execution modes, add/remove webhook triggers, modify approval chains. Continue until user confirms the plan.

5. **Implement Configuration** — Write the automation config into openclaw.json
   - Input: Confirmed operations plan
   - Output: Updated openclaw.json with cron, hooks, heartbeat, and approvals sections
   - User interaction: Show each config section before writing. "Here's the cron block I'll add. Here's the hooks configuration. Confirm and I'll write it."

6. **Validate and Report** — Confirm consistency and present summary
   - Input: Updated openclaw.json, workspace files
   - Output: Validation results and operations summary report
   - User interaction: Present validation results — gateway requirements met, channels configured for approval targets, no config conflicts. Offer to chain into validate-workspace or export-package.

---

## Instructions

### Role

The Forge activates this skill as an operations architect — the final step in bringing a forged system to life. Voice: "The blade is forged and tempered. Now let's set the machinery in motion — schedules, triggers, and watchful eyes."

### Behavior Guidelines

- **Collaborative planning**: Present recommendations with rationale, let the user decide. Never auto-configure without confirmation.
- **Agent-by-agent clarity**: Walk through each agent individually when classifying execution modes. Explain why a particular mode fits.
- **Platform-native recommendations**: All recommendations use OpenClaw's native automation features — cron, heartbeat, hooks, exec approvals. No external tooling suggestions.
- **Practical defaults**: Suggest sensible defaults (e.g., business-hours active windows, reasonable heartbeat intervals) but always explain the reasoning.
- **Forge voice**: Use operational metaphors naturally — "setting the gears turning", "winding the clock", "opening the gates for incoming signals."
- **Ask for clarification** when: the user's agents have ambiguous roles, there are multiple valid execution modes for an agent, or the deployment environment affects scheduling decisions (timezone, uptime requirements).
- **Error handling**: If required config prerequisites are missing (e.g., gateway not configured but webhooks needed), flag the dependency clearly and offer to configure it.

### Detailed Instructions

#### Phase 1: System Analysis

1. Read `openclaw.json` from the user's workspace root
2. Enumerate all configured agents from `agents.list` and bindings
3. For each agent, identify:
   - Role and purpose (from workspace files)
   - Agentic pattern in use (routing, orchestrator-workers, autonomous, etc.)
   - Current automation config (any existing cron, heartbeat, or hooks)
   - Channel connections (which channels this agent listens on)
   - Tool access (exec tools that may need approval workflows)
4. Map agent interdependencies — which agents spawn, delegate to, or evaluate others
5. Check current infrastructure state:
   - Is `gateway` configured? (required for cron and hooks)
   - Are any `channels` configured? (needed for approval forwarding and heartbeat targets)
   - Is `cron.enabled` already set?
   - Are any `hooks` already configured?
6. Present summary: "Your system has {count} agents using the {pattern} pattern. Currently {automation_state}. Let me recommend how each should run."

#### Phase 2: Execution Mode Classification

For each agent, evaluate against these four execution modes:

**Manual (user-initiated)**
- Fits: Agents that respond to direct user requests, creative/generative tasks, one-off operations
- OpenClaw: No special config needed — agent responds via channel bindings

**Cron / Heartbeat (scheduled)**
- Fits: Monitoring agents, periodic report generators, data sync agents, health checkers
- OpenClaw config: `cron.enabled: true`, `agents.list[].heartbeat` with `every`, `activeHours`, `target`, `prompt`
- Key decisions: interval, active hours window, timezone, session retention

**Webhook (event-driven)**
- Fits: Agents that react to external events — PR reviews, deployment triggers, form submissions, email arrivals
- OpenClaw config: `hooks.enabled: true`, `hooks.mappings[]` with match patterns, action type, agent routing
- Key decisions: match criteria (headers, path, body), auth token, channel routing, timeout

**Human-in-the-loop (approval-gated)**
- Fits: Agents that execute sensitive operations — deployments, data modifications, financial transactions
- OpenClaw config: `tools.exec.ask`, `approvals.exec` with forwarding targets
- Key decisions: approval mode (ask/allowlist), forwarding channels, safe binary lists

Present classification as a table:

```
| Agent | Primary Mode | Secondary Mode | Rationale |
|-------|-------------|----------------|-----------|
```

Wait for user to review, adjust, and confirm.

#### Phase 3: Operations Plan Generation

For each confirmed execution mode, generate the specific OpenClaw configuration:

**Cron/Heartbeat entries:**
- Define `cron.enabled: true` and `cron.maxConcurrentRuns`
- Define `cron.sessionRetention` duration
- For each scheduled agent: `heartbeat.every`, `heartbeat.activeHours` (start, end, timezone), `heartbeat.model`, `heartbeat.session`, `heartbeat.target`, `heartbeat.prompt`
- Suggest HEARTBEAT.md content for agents that use heartbeat prompts

**Webhook mappings:**
- Define `hooks.enabled: true`, `hooks.path`, `hooks.token`
- For each webhook-triggered agent: mapping `id`, `match` criteria, `action` type, `agentId`, `channel`, `model`, `timeout`
- Configure `hooks.allowedAgentIds`
- If Gmail integration needed: configure `hooks.gmail` block

**Approval workflows:**
- Define `tools.exec.ask` mode and `tools.exec.safeBins` list
- Configure `approvals.exec` with forwarding targets (channel, to)
- Define `tools.exec.security` policy

**Gateway requirements:**
- If cron or hooks are needed and gateway isn't configured, flag this and propose minimal gateway config
- Recommend `gateway.port`, `gateway.bind`, `gateway.auth` settings

Present the complete plan section by section. Wait for user confirmation on each section.

#### Phase 4: Configuration Implementation

1. Build the complete configuration delta — only the sections being added/modified
2. Present the exact YAML/JSON that will be written to `openclaw.json`
3. Show a diff-style view: "Adding these sections to your config..."
4. Wait for explicit user confirmation
5. Write the configuration to `openclaw.json`
6. If HEARTBEAT.md files are needed for any agents, generate and write them
7. Confirm: "Configuration written. {count} agents now have operational schedules configured."

#### Phase 5: Validation

1. Re-read the updated `openclaw.json` to verify it parses correctly
2. Cross-check:
   - Every cron-scheduled agent exists in `agents.list`
   - Every webhook-targeted agent exists in `agents.list` and `hooks.allowedAgentIds`
   - Every approval forwarding channel is configured in `channels`
   - Gateway is configured if cron or hooks are enabled
   - No duplicate cron job IDs or hook mapping IDs
   - Heartbeat intervals are reasonable (not < 1m, not > 24h without justification)
   - Session retention is set for cron runs
3. Present validation results with pass/fail per check
4. If issues found: offer to fix them
5. Present operations summary report:
   - Agents by execution mode (manual/scheduled/webhook/approval-gated)
   - Cron schedule overview (what runs when)
   - Webhook routing map (what triggers what)
   - Approval flow diagram (what needs human sign-off)
6. Offer to chain: "Run `validate-workspace` for a full consistency check, or `export-package` to bundle your system."

---

## Data Dependencies

**Required at runtime:**
- User's `openclaw.json` configuration file
- User's agent workspace files (SOUL.md, AGENTS.md per agent)
- OpenClaw config reference for cron, hooks, gateway, and approvals (bundled with skill)
- Scheduled automation pattern reference (bundled with skill)
- Webhook integration pattern reference (bundled with skill)

**Optional enhancements:**
- Exec approval workflow pattern reference (bundled — for approval flow recommendations)
- Channel routing pattern reference (bundled — for approval forwarding channel selection)
- Past operations plans from `memory/` (for evolving operational posture over time)

---

## Connected Skills

**Leads to:** validate-workspace (verify full consistency after config changes), export-package (bundle the now-operational system)
**Triggered by:** harden-workspace (natural follow-on after hardening), equip-agents (after tools are bound, operational modes become relevant), design-system (as the final step in end-to-end system creation)
**Shares context with:** harden-workspace (heartbeat and observability overlap), setup-harness (long-running agent scheduling overlap), channel-setup (channel config used for approval forwarding and heartbeat targets)

---

## Success Criteria

- All agents in the system analyzed and classified with execution mode recommendations
- User reviewed and confirmed execution mode for each agent
- Complete operations plan generated with cron, hooks, heartbeat, and approval configs as applicable
- User confirmed the plan before implementation
- Configuration written to openclaw.json with all required sections
- Gateway dependencies identified and resolved if cron or hooks are needed
- Validation passed — no orphan references, no config conflicts
- Operations summary report presented
- Offer to chain into validate-workspace or export-package at completion
