# Forge Skill Registry

**Purpose:** Reference data for The Forge's 9 OpenClaw skills. Used by step-01 for selection display and step-02 for context loading.

---

## Core Skills (Essential)

### design-system

- **Category:** Core
- **Trigger Examples:** "build me a team", "create agents", "I need a system for..."
- **Purpose:** Full multi-agent architecture design and deployment
- **Flow:** Analyze use case → Select agentic pattern → Design agent roster → Generate workspace files per agent → Generate openclaw.json with bindings → Validate → Deploy
- **Data Needs:** Agentic patterns library, OpenClaw config schema, workspace file templates
- **Complexity:** High — most comprehensive skill

### add-agent

- **Category:** Core
- **Trigger Examples:** "add an agent", "I need another agent for..."
- **Purpose:** Add one agent to an existing system
- **Flow:** Read current workspace + config → Ask about new agent → Generate workspace files → Merge config + bindings → Validate
- **Data Needs:** OpenClaw config schema, workspace file templates
- **Complexity:** Medium — works with existing system

### recommend-pattern

- **Category:** Core
- **Trigger Examples:** "what pattern should I use", "how should I architect..."
- **Purpose:** Match use case to agentic pattern
- **Flow:** Analyze requirements → Match against pattern library → Explain trade-offs → Show OpenClaw implementation
- **Data Needs:** Agentic patterns library (primary consumer)
- **Complexity:** Low — advisory, no file generation

---

## Feature Skills (Specialized)

### setup-knowledge

- **Category:** Feature
- **Trigger Examples:** "set up memory", "knowledge graph", "agents should remember..."
- **Purpose:** Tiered memory architecture setup
- **Flow:** Assess needs → Recommend tier (flat-file / vector / graph) → Configure backend → Set up MCP if graph → Configure hooks → Verify
- **Data Needs:** Memory tier comparison data, MCP server configurations, hook templates
- **Complexity:** High — multiple paths based on tier choice

### setup-harness

- **Category:** Feature
- **Trigger Examples:** "long running tasks", "multi-session", "checkpoint..."
- **Purpose:** Long-running agent harness pattern
- **Flow:** Assess task type → Configure progress tracking → Set up heartbeat checkpointing → Configure session bridging → Set up incremental work patterns
- **Data Needs:** Harness configuration templates, heartbeat patterns
- **Complexity:** Medium — focused on one pattern

### harden-workspace

- **Category:** Feature
- **Trigger Examples:** "production ready", "harden", "secure my agents"
- **Purpose:** Systematic production hardening
- **Flow:** Load workspace → Memory config → Tool policies → Failover (model.primary/fallbacks) → Observability (heartbeat) → Self-correction (AGENTS.md) → Boundaries (SOUL.md + sandbox) → Report
- **Data Needs:** Hardening checklist, security best practices, configuration templates
- **Complexity:** High — comprehensive checklist across multiple dimensions

---

## Utility Skills (Support)

### validate-workspace

- **Category:** Utility
- **Trigger Examples:** "validate", "check my setup", "anything wrong?"
- **Purpose:** Cross-artifact validation
- **Flow:** Load workspace → Structural checks → Coherence checks → Hardening checks → Report with recommendations
- **Data Needs:** Validation rules, structural requirements, coherence criteria
- **Complexity:** Medium — read-only analysis

### export-package

- **Category:** Utility
- **Trigger Examples:** "export", "package", "share my setup"
- **Purpose:** Bundle workspace for sharing
- **Flow:** Load workspace → Inject metadata → Generate setup prompt → Bundle .ocf.zip
- **Data Needs:** Package manifest template, setup prompt template
- **Complexity:** Low — packaging operation

### import-package

- **Category:** Utility
- **Trigger Examples:** "import", "install package"
- **Purpose:** Install workspace package
- **Flow:** Receive .ocf.zip → Validate contents → Install files → Merge config → Verify
- **Data Needs:** Package validation rules, merge conflict resolution logic
- **Complexity:** Medium — merge handling

---

## Skill Connections

```
recommend-pattern --> design-system --> setup-knowledge
                                   --> setup-harness
                                   --> harden-workspace
                                   --> validate-workspace
                                   --> export-package

                     add-agent -----> harden-workspace
                                   --> validate-workspace

                     import-package -> validate-workspace
```

---

## Agentic Patterns Reference

| Pattern | When to Use | OpenClaw Implementation |
|---------|-------------|----------------------|
| Prompt Chaining | Tasks decomposable into fixed sequential steps | Sequential `sessions_spawn` with task handoff |
| Routing | Distinct input categories needing specialist handling | `bindings[]` with match rules + specialist agents |
| Parallelization | Speed priority or multiple perspectives needed | Multiple `sessions_spawn` + `subagents.maxConcurrent` |
| Orchestrator-Workers | Complex tasks with unpredictable subtasks | Parent agent dynamically spawns workers via `sessions_spawn` |
| Evaluator-Optimizer | Clear evaluation criteria, iterative refinement valuable | Reviewer sub-agent, critique loop via `sessions_send` |
| Autonomous Agent | Open-ended problems, unpredictable step count | Tool use + heartbeat feedback loop |
| Long-Running Harness | Multi-session tasks needing progress persistence | Progress log in `memory/`, heartbeat checkpointing, incremental sessions |
