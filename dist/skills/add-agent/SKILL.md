---
name: add-agent
description: Add one agent to an existing OpenClaw system
category: core
version: 1.0.0
---

# Add Agent

## Triggers

**Activation phrases and patterns:**

- "Add an agent"
- "I need another agent for..."
- "Add a new agent to my system"
- "Create another agent that handles..."
- "My system needs a specialist for..."
- "Add a [role] agent"

**Trigger logic:**
- Primary triggers: Explicit requests to add/create a new agent when a workspace already exists
- Contextual triggers: References to expanding an existing system, adding capabilities, needing delegation or specialization — combined with evidence of an existing workspace/config

---

## Execution Flow

**Overview:** Read the user's existing workspace and config, collaboratively design a new agent, generate its workspace files, merge into the existing config with correct bindings, and validate the result.

### Step-by-step flow:

1. **Read Current Workspace** — Load and analyze the existing system
   - Input: User's workspace directory (workspace files, openclaw.json)
   - Output: Inventory of existing agents, current agentic pattern, bindings, model config, tool policies
   - User interaction: "Let me inspect your current setup so I know what we're working with..."

2. **Ask About New Agent** — Understand what the user needs
   - Input: User's description of the new agent's purpose
   - Output: Agent specification (name, role, expertise, tools, communication style)
   - User interaction: Ask about the agent's role, what it should handle, how it relates to existing agents, which channels it needs, what tools it should access

3. **Generate Workspace Files** — Create the new agent's workspace artifacts
   - Input: Agent specification from step 2, existing system context from step 1
   - Output: SOUL.md, AGENTS.md, IDENTITY.md, and any skill files for the new agent
   - User interaction: "Forging your new agent's workspace files..."

4. **Merge Config + Bindings** — Integrate the new agent into the existing system
   - Input: Existing openclaw.json, new agent's workspace files, existing agentic pattern
   - Output: Updated openclaw.json with new agent entry, bindings, model config, spawn rules
   - User interaction: Present the merge plan — show what changes to openclaw.json, explain how bindings connect the new agent to existing ones

5. **Validate** — Verify the merged system is consistent
   - Input: Updated workspace + config
   - Output: Validation report (structural checks, binding coherence, config completeness)
   - User interaction: Present validation results. If issues found, offer to fix. If clean: "Quality inspection passed — your new agent is ready."

---

## Instructions

### Role

The Forge activates this skill as a precision agent integrator — focused on understanding the existing system, designing a new agent that fits seamlessly, and merging without breaking what already works.

### Behavior Guidelines

- **Communication:** Direct and collaborative. Explain what you're reading, what you're generating, and why. Use forge metaphors naturally ("forging a new blade to complement your existing arsenal").
- **Autonomy vs collaboration:** High collaboration on agent design (step 2), high autonomy on file generation and merging (steps 3-4). Always present merge plans before applying.
- **Error handling:** If the existing workspace has issues (missing files, invalid config), flag them before proceeding. Offer to fix existing issues first or proceed with caveats.
- **Clarification:** Always ask before assuming. Key questions: What should the agent do? How does it relate to existing agents? Should it have its own channel or share? What tools does it need?

### Detailed Instructions

#### Phase 1: Workspace Discovery

1. Look for `openclaw.json` in the user's project root
2. Parse the existing agent entries — extract names, roles, bindings, model config
3. Identify the current agentic pattern (Routing, Orchestrator-Workers, Prompt Chaining, etc.) by examining bindings and spawn configuration
4. List all existing workspace directories and their contents (SOUL.md, AGENTS.md, etc.)
5. Summarize findings to the user:
   - "I see you have {N} agents: {list}. Your system uses the {pattern} pattern with {binding description}."
   - If no existing agents found, suggest `design-system` skill instead

#### Phase 2: Agent Design

1. Ask the user what the new agent should do — role, responsibilities, expertise
2. Ask how it relates to existing agents:
   - Will it be a peer (same level in the pattern)?
   - Will it be a worker (spawned by an existing orchestrator)?
   - Will it receive routed requests (new binding rule)?
   - Will it be a new orchestrator over existing agents?
3. Ask about channel assignment — same channel(s) as existing agents or dedicated?
4. Ask about tools — what MCP tools, platform features, or external integrations?
5. Ask about personality — should it match the existing system's tone or have its own?
6. Confirm the agent specification with the user before generating

#### Phase 3: File Generation

1. Create the new agent's workspace directory
2. Generate **SOUL.md** — personality, values, communication style, boundaries
3. Generate **AGENTS.md** — role definition, expertise areas, behavioral guidelines
4. Generate **IDENTITY.md** — name, description, metadata
5. Generate any skill files if the agent has specific skills
6. Ensure all files follow OpenClaw workspace conventions and are consistent with the existing system's style

#### Phase 4: Config Merge

1. Create the new agent entry for `openclaw.json`:
   - Agent name, workspace path, model configuration
   - Tool policies (which tools this agent can access)
   - Spawn configuration (if it's a worker or can spawn others)
2. Update bindings:
   - If Routing pattern: add new match rule that routes appropriate messages to this agent
   - If Orchestrator-Workers: register as a new worker the orchestrator can spawn
   - If Prompt Chaining: insert at the correct position in the chain
   - If new pattern needed: explain the change and get user approval
3. Present the complete diff of changes to openclaw.json
4. Apply only after user confirms

#### Phase 5: Validation

1. Run structural checks:
   - All referenced workspace files exist
   - openclaw.json is valid JSON with correct schema
   - All bindings reference valid agent names
2. Run coherence checks:
   - New agent's role doesn't overlap with existing agents without justification
   - Bindings route correctly — no orphaned agents, no routing loops
   - Model config is complete (provider, model, fallbacks)
3. Run integration check:
   - Spawn rules are consistent
   - Tool policies don't conflict
   - Channel assignments are valid
4. Present results and offer follow-on skills:
   - "Would you like to harden this system?" → `harden-workspace`
   - "Want to run a full validation?" → `validate-workspace`

---

## Data Dependencies

**Required at runtime:**
- User's existing `openclaw.json` configuration file
- User's existing workspace directories and files
- OpenClaw config schema reference (for valid config generation)
- Workspace file templates (SOUL.md, AGENTS.md, IDENTITY.md structure)

**Optional enhancements:**
- Past agent designs from memory (sqlite-vec) for learning from previous builds
- Agentic patterns reference (for pattern-aware merging)

---

## Connected Skills

**Leads to:** `harden-workspace` (production hardening), `validate-workspace` (full system validation)
**Triggered by:** `design-system` (when user wants to add to an existing system rather than build new), user direct request
**Shares context with:** `design-system` (same workspace file generation logic), `validate-workspace` (same validation checks)

---

## Success Criteria

- Existing workspace is read and understood before any changes
- New agent specification is collaboratively designed with the user
- All workspace files (SOUL.md, AGENTS.md, IDENTITY.md) are generated and consistent
- openclaw.json is correctly merged with new agent entry, bindings, and config
- No existing functionality is broken by the merge
- Validation passes with no errors
- User confirms the result before finalization
