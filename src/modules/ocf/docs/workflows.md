# Workflows Reference

OCF includes 11 workflows organized by category:

---

## Core Workflows

### create-agent-brief

**Workflow:** `create-agent-brief`

**Purpose:**
Guided discovery of a new OpenClaw agent system (single or multi-agent). Produces a structured brief covering agents, personas, skills, channels, orchestration, memory architecture, resilience needs, and safety requirements.

**When to Use:**
Starting a new multi-agent system from scratch. This is the recommended entry point for any non-trivial agent system.

**Key Steps:**
1. Concept gathering
2. Agent roster design
3. Skill & channel mapping
4. Orchestration planning
5. Memory & resilience design
6. Brief assembly

**Agent(s):** Vulcan (Forge Master)

---

### create-agent-system

**Workflow:** `create-agent-system`

**Purpose:**
Takes a structured brief and generates the complete OpenClaw workspace with all artifacts for every agent in the system.

**When to Use:**
After completing a brief with create-agent-brief. This is the main generation workflow.

**Key Steps:**
1. Load and validate brief
2. Generate identities (SOUL.md, AGENTS.md)
3. Generate context (USER.md, MEMORY.md)
4. Generate skills
5. Generate configuration
6. Add self-correction directives
7. Assemble workspace
8. User review

**Agent(s):** Anima (Soul Smith), Cog (Gear Wright)

---

### create-single-agent

**Workflow:** `create-single-agent`

**Purpose:**
Streamlined workflow combining brief and generation for a single agent workspace.

**When to Use:**
When you need just one agent and want a faster, simpler flow.

**Key Steps:**
1. Quick brief (concept, persona, skills, channels in one pass)
2. Identity & config generation
3. Assembly and review

**Agent(s):** Anima (Soul Smith)

---

## Feature Workflows

### design-orchestration

**Workflow:** `design-orchestration`

**Purpose:**
Design multi-agent communication patterns: spawn/send relationships, session routing, channel bindings, handoff protocols, failure handling, loop prevention, and subagent tool restrictions.

**When to Use:**
When designing or redesigning how agents in a system communicate and coordinate.

**Key Steps:**
1. Agent relationship mapping
2. Communication pattern design
3. Channel binding configuration
4. Failure handling design
5. Subagent policy definition

**Agent(s):** Vulcan (Forge Master)

---

### create-skill

**Workflow:** `create-skill`

**Purpose:**
Generate a complete OpenClaw skill with SKILL.md, executable scaffold, and gating rules. Ensures security scanner compliance.

**When to Use:**
When adding a new skill to an agent, whether during system creation or as an enhancement.

**Key Steps:**
1. Skill requirements gathering
2. Gating rule definition
3. Code scaffold generation
4. SKILL.md assembly

**Agent(s):** Cog (Gear Wright)

---

### edit-agent-system

**Workflow:** `edit-agent-system`

**Purpose:**
Modify an existing generated workspace while maintaining coherence across all artifacts.

**When to Use:**
When you need to change an agent's persona, skills, or configuration and want the implications propagated correctly.

**Key Steps:**
1. Load existing workspace
2. Identify desired changes
3. Impact analysis
4. Apply changes with propagation
5. Coherence verification

**Agent(s):** Anima (Soul Smith), Cog (Gear Wright)

---

### configure-production-hardening

**Workflow:** `configure-production-hardening`

**Purpose:**
Layer production features onto any OpenClaw workspace: memory config, tool policies, failover, heartbeat, logging, self-correction, and boundary rules.

**When to Use:**
When preparing a workspace for production use, or hardening an existing workspace not created by OCF.

**Key Steps:**
1. Load workspace and assess current hardening
2. Memory backend configuration
3. Tool policy definition
4. Failover & resilience setup
5. Observability configuration
6. Self-correction directive generation
7. Boundary rule definition

**Agent(s):** Cog (Gear Wright)

---

## Utility Workflows

### validate-workspace

**Workflow:** `validate-workspace`

**Purpose:**
Check a workspace for internal consistency: persona/directive alignment, skill presence, binding completeness, memory directives, tool policies, boundaries, failover, and self-correction.

**When to Use:**
After generating or editing a workspace, before deployment.

**Key Steps:**
1. Load and inventory workspace
2. Structural checks
3. Cross-artifact coherence checks
4. Hardening checks
5. Validation report

**Agent(s):** Cog (Gear Wright)

---

### export-config

**Workflow:** `export-config`

**Purpose:**
Extract openclaw.json configuration fragments from a workspace, formatted for merge into an existing OpenClaw installation.

**When to Use:**
When integrating a generated workspace into an existing OpenClaw setup.

**Key Steps:**
1. Load workspace
2. Extract configuration fragments
3. Format for merge

**Agent(s):** Cog (Gear Wright)

---

### package-export

**Workflow:** `package-export`

**Purpose:**
Bundle a completed workspace into a portable `.ocf.zip` + companion `setup.md` for deployment on any OpenClaw instance.

**When to Use:**
When sharing an agent system or deploying to a different OpenClaw instance.

**Key Steps:**
1. Load and validate workspace
2. Inject OCF metadata
3. Generate setup prompt
4. Bundle into .ocf.zip

**Agent(s):** Cog (Gear Wright)

---

### package-import

**Workflow:** `package-import`

**Purpose:**
Receive an `.ocf.zip` + setup prompt and install the agent system on a running OpenClaw instance.

**When to Use:**
When receiving a shared agent system package for deployment.

**Key Steps:**
1. Receive and validate package
2. Extract workspace files
3. Merge configuration
4. Register agents and bindings
5. Activate and verify

**Agent(s):** Cog (Gear Wright)
