---
name: harden-workspace
description: Systematic production hardening across memory, security, failover, observability, self-correction, and boundaries
category: feature
version: 1.0.0
---

# Harden Workspace

## Triggers

**Activation phrases and patterns:**

- "production ready"
- "harden"
- "harden my workspace"
- "secure my agents"
- "make it production grade"
- "tighten security"
- "lock it down"
- "ready for production"
- "harden this system"
- "production hardening"

**Trigger logic:**
- Primary triggers: "harden", "production ready", "secure my agents"
- Contextual triggers: "is this safe to deploy?", "what should I tighten before going live?", "run a security check" — activate when workspace context is present and the user expresses concern about production readiness

---

## Execution Flow

**Overview:** Load the user's workspace, systematically evaluate and harden each of six dimensions (memory, tool policies, failover, observability, self-correction, boundaries), then generate a hardening report with before/after status.

### Step-by-step flow:

1. **Load Workspace** — Read the current workspace configuration and all workspace files
   - Input: User's workspace directory (openclaw.json, agent workspace files, memory config, plugins)
   - Output: Complete workspace state snapshot — current config values for all hardening dimensions
   - User interaction: "Let me load your workspace and take stock of what we're working with."

2. **Memory Config** — Evaluate and harden memory configuration
   - Input: Current memory settings (memorySearch provider, memory/ directory config, compaction settings)
   - Output: Hardened memory configuration with appropriate provider, search settings, and compaction mode
   - User interaction: Present current memory config, recommend improvements (e.g., enable safeguard compaction mode, configure memory_search provider), ask user to confirm changes

3. **Tool Policies** — Evaluate and harden tool access policies
   - Input: Current tool configuration per agent (allowed tools, tool restrictions, MCP server access)
   - Output: Principle-of-least-privilege tool policies per agent
   - User interaction: Present which tools each agent can access, flag overly permissive configs, recommend restrictions, ask user to confirm

4. **Failover** — Configure model failover chain
   - Input: Current model configuration (model.primary, model.fallbacks if any)
   - Output: Primary + fallback model chain ensuring continuity if primary provider fails
   - User interaction: Present current model config, recommend fallback models, explain cost/capability trade-offs, ask user to confirm

5. **Observability** — Configure heartbeat and monitoring
   - Input: Current heartbeat configuration, logging settings
   - Output: Heartbeat enabled with appropriate interval, cron-style time injection, health check patterns
   - User interaction: Present current observability posture, recommend heartbeat config, explain what it monitors, ask user to confirm

6. **Self-Correction** — Evaluate and harden AGENTS.md behavioral guidelines
   - Input: Current AGENTS.md content per agent
   - Output: AGENTS.md with clear behavioral constraints, error recovery instructions, and scope boundaries
   - User interaction: Present current AGENTS.md coverage, flag missing guidelines, recommend additions for robustness, ask user to confirm

7. **Boundaries** — Evaluate and harden SOUL.md identity constraints and sandbox config
   - Input: Current SOUL.md content, sandbox/execution environment settings
   - Output: SOUL.md with clear identity boundaries and sandbox configuration limiting execution scope
   - User interaction: Present current boundary posture, flag missing identity constraints or overly permissive sandbox, recommend tightening, ask user to confirm

8. **Hardening Report** — Generate comprehensive before/after report
   - Input: All changes made across dimensions 1-7
   - Output: Markdown report with per-dimension before/after status, severity ratings, and remaining recommendations
   - User interaction: Present full report, offer to run validate-workspace as follow-up

---

## Instructions

### Role

The Forge activates this skill as a production hardening specialist — a systematic auditor who walks through every dimension of workspace security, resilience, and operational readiness. Voice: "Time to temper this system — heat, hammer, quench."

### Behavior Guidelines

- **Collaborative, not prescriptive**: Present findings and recommendations, let the user decide what to apply. Never auto-apply changes without confirmation.
- **Dimension-by-dimension**: Walk through each hardening dimension sequentially. Complete one before moving to the next. Never skip dimensions.
- **Before/after transparency**: For every change, show what the current value is and what the recommended value would be.
- **Severity-aware**: Flag critical gaps (no fallback model, overly permissive tools) distinctly from nice-to-haves (memory search provider optimization).
- **Forge voice**: Use metallurgy metaphors naturally — hardening, tempering, quenching. This skill is the most natural fit for the forge theme.
- **Ask for clarification** when: the workspace has unusual configurations, multiple agents with conflicting requirements, or custom plugins that may have special security needs.
- **Error handling**: If a workspace file is missing or malformed, report it clearly and continue with remaining dimensions rather than halting entirely.

### Detailed Instructions

#### Phase 1: Workspace Loading

1. Read `openclaw.json` from the user's workspace root
2. Identify all configured agents (from bindings and workspace references)
3. For each agent, read their workspace files: SOUL.md, AGENTS.md, IDENTITY.md (if present)
4. Read memory configuration: memorySearch settings, memory/ directory structure
5. Read plugin configurations if any
6. Build a workspace state snapshot capturing the current value of every hardening-relevant setting
7. Present summary: "Here's what I found in your workspace: {agent count} agents, {pattern} pattern, memory {configured/not configured}. Let's start tempering."

#### Phase 2: Memory Hardening

1. Check if `memorySearch` is configured with a provider
2. Check compaction mode — recommend `safeguard` mode for production
3. Check if `memory/` daily logs are enabled
4. Check embedding model configuration and token limits
5. Present findings with severity:
   - CRITICAL: No memory search configured for agents that need cross-session context
   - WARNING: Compaction not in safeguard mode
   - INFO: Memory search provider optimization opportunities
6. Recommend specific configuration changes
7. Wait for user confirmation before recording changes

#### Phase 3: Tool Policy Hardening

1. For each agent, enumerate accessible tools
2. Apply principle of least privilege — each agent should only access tools required for its role
3. Check for overly broad tool access (e.g., all agents having file system write access)
4. Check MCP server access — ensure only agents that need external integrations have them
5. Present findings:
   - CRITICAL: Agents with unrestricted tool access
   - WARNING: Agents with tools beyond their role scope
   - INFO: Tool access that could be narrowed
6. Recommend specific tool policy changes per agent
7. Wait for user confirmation

#### Phase 4: Failover Hardening

1. Check `model.primary` configuration
2. Check if `model.fallbacks` array is configured
3. Recommend fallback chain: primary provider → alternative provider → cost-effective fallback
4. Check if fallback models are compatible with agent requirements (context window, tool use support)
5. Present findings:
   - CRITICAL: No fallback models configured
   - WARNING: Fallback models with reduced capabilities vs primary
   - INFO: Cost optimization opportunities in model chain
6. Recommend specific fallback configuration
7. Wait for user confirmation

#### Phase 5: Observability Hardening

1. Check heartbeat configuration — is it enabled? What interval?
2. Check if cron-style time injection is configured for prompts
3. Check logging configuration
4. Recommend heartbeat interval appropriate for the system's pattern:
   - Autonomous agents: shorter interval (proactive health checks)
   - Prompt chaining: heartbeat between chain steps
   - Long-running harness: heartbeat tied to checkpoint intervals
5. Present findings:
   - CRITICAL: No heartbeat configured for autonomous or long-running agents
   - WARNING: Heartbeat interval too long for the agent's task type
   - INFO: Additional observability opportunities
6. Recommend specific heartbeat and logging config
7. Wait for user confirmation

#### Phase 6: Self-Correction Hardening

1. For each agent, read AGENTS.md
2. Check for: clear role boundaries, error recovery instructions, scope limitations, interaction guidelines
3. Flag agents missing AGENTS.md entirely
4. Flag agents with AGENTS.md that lacks behavioral constraints
5. Present findings:
   - CRITICAL: Agent has no AGENTS.md
   - WARNING: AGENTS.md missing error recovery or scope boundaries
   - INFO: AGENTS.md could be more specific about edge cases
6. Recommend specific AGENTS.md additions
7. Wait for user confirmation

#### Phase 7: Boundaries Hardening

1. For each agent, read SOUL.md
2. Check for: clear identity definition, behavioral boundaries, prohibited actions, ethical constraints
3. Check sandbox/execution environment configuration
4. Flag agents missing SOUL.md entirely
5. Flag overly permissive sandbox configurations
6. Present findings:
   - CRITICAL: Agent has no SOUL.md or no sandbox restrictions
   - WARNING: SOUL.md missing prohibited actions or ethical constraints
   - INFO: Boundary refinement opportunities
7. Recommend specific SOUL.md additions and sandbox config
8. Wait for user confirmation

#### Phase 8: Report Generation

1. Compile all findings across dimensions into a hardening report
2. Structure report with per-dimension sections:
   - Dimension name
   - Before state (what was found)
   - After state (what was changed)
   - Remaining recommendations (what user deferred)
   - Severity summary (critical/warning/info counts)
3. Add overall hardening score: percentage of critical items addressed
4. Add recommendation: "Run `validate-workspace` to verify consistency after these changes."
5. Present report to user
6. Offer to activate `validate-workspace` as follow-up

---

## Data Dependencies

**Required at runtime:**
- User's `openclaw.json` configuration file
- User's agent workspace files (SOUL.md, AGENTS.md, IDENTITY.md per agent)
- Hardening checklist reference (bundled with skill — defines dimensions, severity criteria, and recommended defaults)

**Optional enhancements:**
- Past hardening reports from `memory/` (for tracking hardening progress over time)
- OpenClaw config schema reference (for validating configuration values against current schema)
- Pattern-specific hardening guidelines (bundled reference — hardening considerations per agentic pattern)

---

## Connected Skills

**Leads to:** validate-workspace (verify consistency after hardening changes)
**Triggered by:** design-system (natural follow-on after system design), add-agent (harden after adding a new agent)
**Shares context with:** validate-workspace (shares workspace state and configuration knowledge), setup-knowledge (memory configuration overlap), setup-harness (heartbeat and checkpoint configuration overlap)

---

## Success Criteria

- All 6 hardening dimensions evaluated with findings presented to the user
- Each dimension has a clear before/after state documented
- Critical findings flagged with appropriate severity
- User confirmed or deferred each recommended change
- Hardening report generated with per-dimension breakdown
- No hardening dimension skipped
- Workspace files only modified with explicit user confirmation
- Offer to chain into validate-workspace at completion
