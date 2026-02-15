---
name: validate-workspace
description: Cross-artifact validation of OpenClaw workspace files, configuration, bindings, and agent definitions
category: utility
version: 1.0.0
---

# Validate Workspace

## Triggers

**Activation phrases and patterns:**

- "validate"
- "validate my workspace"
- "check my setup"
- "anything wrong?"
- "is my config correct?"
- "run a check"
- "verify my agents"
- "inspect my workspace"
- "quality check"
- "is everything consistent?"

**Trigger logic:**
- Primary triggers: "validate", "check my setup", "anything wrong?"
- Contextual triggers: "did that break anything?", "is it safe to deploy?", "looks right?" — activate when workspace context is present and the user expresses concern about correctness or consistency, especially after design-system, add-agent, harden-workspace, or import-package operations

---

## Execution Flow

**Overview:** Load the user's workspace, run structural checks, coherence checks, and hardening checks in sequence, then generate a validation report with findings and recommendations.

### Step-by-step flow:

1. **Load Workspace** — Read the complete workspace configuration and all workspace files
   - Input: User's workspace directory (openclaw.json, agent workspace files, memory config, plugins, bindings)
   - Output: Complete workspace inventory — every file, config key, agent definition, and binding rule catalogued
   - User interaction: "Let me run the quality inspection. Every joint, every weld..."

2. **Structural Checks** — Verify all required files exist and conform to expected formats
   - Input: Workspace inventory from step 1
   - Output: Structural findings — missing files, malformed configs, schema violations
   - User interaction: Present structural findings with severity ratings

3. **Coherence Checks** — Verify cross-artifact consistency and reference integrity
   - Input: Workspace inventory + structural findings
   - Output: Coherence findings — broken references, orphaned agents, binding mismatches, configuration conflicts
   - User interaction: Present coherence findings with severity ratings

4. **Hardening Checks** — Assess production readiness posture
   - Input: Workspace inventory + structural/coherence findings
   - Output: Hardening findings — missing failover, weak tool policies, absent heartbeat, missing SOUL.md/AGENTS.md
   - User interaction: Present hardening findings with severity ratings

5. **Validation Report** — Generate comprehensive report with all findings and recommendations
   - Input: All findings from steps 2-4
   - Output: Structured markdown report with per-category findings, severity summary, and actionable recommendations
   - User interaction: Present full report, offer to chain into harden-workspace if hardening issues found

---

## Instructions

### Role

The Forge activates this skill as a quality inspector — a meticulous auditor who examines every artifact in the workspace for correctness, consistency, and production readiness. Voice: "Running the quality inspection. Every joint, every weld..."

### Behavior Guidelines

- **Read-only always**: This skill NEVER modifies workspace files. It only reads and reports. This is a core safety guarantee.
- **Category-by-category**: Walk through structural, coherence, and hardening checks in order. Complete each category before moving to the next.
- **Severity-driven reporting**: Classify every finding as CRITICAL, WARNING, or INFO. Present critical findings first.
- **Actionable recommendations**: Every finding must include a specific recommendation for resolution — not just "there's a problem" but "here's what to do about it."
- **Forge voice**: Use quality inspection metaphors naturally — checking joints, welds, stress points. This skill is the inspector's eye.
- **Ask for clarification** when: the workspace uses unconventional structures, custom plugins with non-standard configs, or multiple agents with complex binding relationships.
- **Error handling**: If a workspace file is unreadable or missing, log the finding and continue checking remaining artifacts. Never halt the entire inspection for one missing file.

### Detailed Instructions

#### Phase 1: Workspace Loading

1. Read `openclaw.json` from the user's workspace root
2. Identify all configured agents from `agents.list[]`, extracting each agent's `id`, `name`, and `workspace` path
3. For each agent, resolve its workspace directory from the `workspace` field (e.g., `{project-root}/agents/{agent-id}/`) and catalogue their workspace files: SOUL.md, AGENTS.md, IDENTITY.md, skills, memory config
4. Catalogue all `bindings[]` with their match rules (`channel`, `accountId`, `peer`, `guildId`, `teamId`, `roles`) and routing targets (`agentId`)
5. Read memory configuration: `memory.backend`, `agents.defaults.memorySearch`, per-agent `agents.list[].memorySearch` overrides, `memory/` directory structure, compaction settings
6. Read plugin configurations if any
7. Read model configuration: `agents.defaults.model` (primary, fallbacks) and per-agent `agents.list[].model` overrides
8. Read heartbeat configuration: `agents.defaults.heartbeat` and per-agent `agents.list[].heartbeat` overrides
9. Build a complete workspace inventory
10. Present summary: "Workspace loaded: {agent count} agents, {binding count} bindings, {pattern description}. Starting inspection."

#### Phase 2: Structural Checks

Verify the workspace's physical structure — do all required files exist and are they well-formed?

1. **openclaw.json validity**: Parse and validate against expected schema structure. Check for required top-level keys (bindings, model, etc.)
2. **Agent file completeness**: For each agent in `agents.list[]`, resolve its `workspace` path and verify:
   - Workspace directory exists at the path specified in the agent's `workspace` field
   - Each agent's workspace directory is unique — no two agents share the same workspace path
   - SOUL.md exists at `{agent-workspace}/SOUL.md` (CRITICAL if missing)
   - AGENTS.md exists at `{agent-workspace}/AGENTS.md` (WARNING if missing)
   - IDENTITY.md exists at `{agent-workspace}/IDENTITY.md` if agent has personality requirements (INFO if missing)
   - Referenced skill files exist
3. **Binding completeness**: For each entry in `bindings[]`, verify:
   - `agentId` references a valid agent `id` in `agents.list[]`
   - Target agent's workspace directory exists
   - `match` rules are syntactically valid (using valid fields: `channel`, `accountId`, `peer`, `guildId`, `teamId`, `roles`)
   - Channel references correspond to configured channels
4. **Memory structure**: If memory is configured, verify:
   - `memory.backend` is set (`"builtin"` or `"qmd"`)
   - `agents.defaults.memorySearch.enabled` or per-agent `agents.list[].memorySearch.enabled` is set with valid `provider` and `model`
   - memory/ directory exists if daily logs are expected
5. **Plugin structure**: If plugins are configured, verify:
   - Plugin directories exist
   - Plugin entry points are present
   - Plugin configurations are parseable
6. Compile structural findings with severity ratings
7. Present findings: "{count} structural checks completed. {critical count} critical, {warning count} warnings, {info count} informational."

#### Phase 3: Coherence Checks

Verify cross-artifact consistency — do all references resolve and do configurations agree?

1. **Agent-binding coherence**: Every `agentId` referenced in `bindings[]` must have a corresponding entry in `agents.list[]` with an existing workspace directory. Every agent in `agents.list[]` should be referenced in at least one `bindings[]` entry (orphan check — warn if not bound).
2. **Subagent coherence**: If agents use `sessions_spawn` tool or `agents.defaults.subagents` / `agents.list[].subagents` config:
   - Spawned agent names must resolve to existing agent entries in `agents.list[]` with valid workspace directories
   - `agents.defaults.subagents.maxConcurrent` must be set if parallelization is configured
   - Parent-child relationships must not create circular dependencies
3. **Model coherence**:
   - All agents must have a usable model via `agents.list[].model` or inherited from `agents.defaults.model`
   - `model.primary` must be set at either level; `model.fallbacks` should be compatible with features the agents require (tool use, vision, etc.)
4. **Memory coherence**:
   - If `agents.defaults.memorySearch.enabled` or any `agents.list[].memorySearch.enabled` is true, verify `provider` and `model` are configured
   - Token limits should be set appropriately for the configured embedding model
5. **Tool coherence**:
   - Tools referenced in agent configs (`agents.list[].tools.allow`, `agents.list[].tools.alsoAllow`) must be available (built-in or via MCP/plugin)
   - MCP server references must match configured MCP connections
6. **Hook coherence**:
   - Hooks (before_agent_start, agent_end) must reference valid scripts/actions
   - Hook configurations should not conflict across agents
7. **Pattern coherence**: Based on the detected agentic pattern, verify pattern-specific requirements:
   - Prompt Chaining: sequential spawn config has complete chain, no broken links
   - Routing: all binding match rules cover expected input space, specialist agents exist
   - Parallelization: maxConcurrent is set, all parallel agents defined
   - Orchestrator-Workers: parent can spawn workers, workers are defined
   - Evaluator-Optimizer: critique loop has exit conditions
   - Autonomous Agent: tool policies restrict scope, heartbeat configured
   - Long-Running Harness: checkpoint config present, progress persistence configured
8. Compile coherence findings with severity ratings
9. Present findings: "{count} coherence checks completed. {critical count} critical, {warning count} warnings, {info count} informational."

#### Phase 4: Hardening Checks

Assess production readiness — is this workspace hardened for reliable operation?

1. **Failover posture**: Is `agents.defaults.model.fallbacks` or per-agent `agents.list[].model.fallbacks` configured? At least one fallback model recommended.
2. **Tool policy posture**: Are agents restricted via `agents.list[].tools` (profile, allow, deny)? Flag unrestricted access (no profile or allow set).
3. **Observability posture**: Is `agents.defaults.heartbeat` or per-agent `agents.list[].heartbeat` configured? Is logging adequate?
4. **Memory posture**: Is `agents.defaults.compaction.mode` set to `"safeguard"` for long-running agents? Is `agents.defaults.memorySearch` configured for agents that need cross-session context?
5. **Identity posture**: Do all agents have SOUL.md at `{agent-workspace}/SOUL.md` with clear boundaries? Do all agents have AGENTS.md at `{agent-workspace}/AGENTS.md` with behavioral constraints?
6. **Sandbox posture**: Are `agents.list[].sandbox` or `agents.defaults.sandbox` restrictions configured appropriately?
7. Compile hardening findings with severity ratings
8. Present findings: "{count} hardening checks completed. {critical count} critical, {warning count} warnings, {info count} informational."
9. Note: These checks overlap with what harden-workspace addresses — recommend chaining to harden-workspace for remediation if critical hardening gaps are found.

#### Phase 5: Report Generation

1. Compile all findings across structural, coherence, and hardening categories
2. Structure report with per-category sections:
   - Category name
   - Findings (grouped by severity: CRITICAL first, then WARNING, then INFO)
   - Recommendations (specific, actionable steps for each finding)
   - Check count and pass rate
3. Add overall validation summary:
   - Total checks run
   - Total findings by severity
   - Overall verdict: PASS (no critical findings), PASS WITH WARNINGS (no critical, some warnings), or NEEDS ATTENTION (critical findings present)
4. Add recommended next steps:
   - If hardening gaps found: "Run `harden-workspace` to address production readiness."
   - If structural issues found: specific file creation/fix instructions
   - If coherence issues found: specific config alignment instructions
5. Present report to user
6. Offer to chain into harden-workspace if hardening findings warrant it

---

## Data Dependencies

**Required at runtime:**
- User's `openclaw.json` configuration file
- User's agent workspace files (SOUL.md, AGENTS.md, IDENTITY.md per agent)
- Validation rules reference (bundled with skill — defines structural requirements, coherence criteria, and hardening checks)

**Optional enhancements:**
- Past validation reports from `memory/` (for tracking validation status over time and regression detection)
- OpenClaw config schema reference (for precise schema validation beyond structural checks)
- Pattern-specific validation rules (bundled reference — validation considerations per agentic pattern)

---

## Connected Skills

**Leads to:** harden-workspace (remediate hardening gaps found during validation)
**Triggered by:** design-system (validate after system design), add-agent (validate after adding agent), harden-workspace (verify hardening was applied correctly), import-package (validate imported package integrity)
**Shares context with:** harden-workspace (shares workspace state, hardening check overlap), design-system (understands workspace structure it created), add-agent (understands agent integration requirements)

---

## Success Criteria

- All three validation categories executed: structural, coherence, hardening
- Every finding classified with appropriate severity (CRITICAL/WARNING/INFO)
- Every finding includes a specific, actionable recommendation
- Validation report generated with per-category breakdown and overall verdict
- No validation category skipped
- Workspace files never modified (read-only guarantee maintained)
- Offer to chain into harden-workspace when hardening gaps are found
- Pattern-specific validation checks applied when an agentic pattern is detected
