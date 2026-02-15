# The Forge — User Guide

> **"Where they were many, I am one. Where they worked in turns, I work as a whole."**

The Forge is a meta-agent that designs, builds, configures, and deploys multi-agent AI systems on [OpenClaw](https://github.com/open-claw). You describe what you need in natural language — The Forge selects the right agentic pattern, designs your agent team, generates production-ready configuration, and guides deployment. No config files to edit. No architecture decisions to agonize over.

---

## Table of Contents

- [Quick Start](#quick-start)
- [How It Works](#how-it-works)
- [Skills Reference](#skills-reference)
  - [Design Phase](#design-phase)
  - [Enablement Phase](#enablement-phase)
  - [Hardening & Operations](#hardening--operations)
  - [Validation & Packaging](#validation--packaging)
- [Workspace Files](#workspace-files)
- [Agentic Patterns](#agentic-patterns)
- [Examples](#examples)
- [Build Artifacts](#build-artifacts)
- [Troubleshooting](#troubleshooting)

---

## Quick Start

### 1. Install

```bash
bmad install forge
```

### 2. Talk to The Forge

Open your preferred channel (Discord, Telegram, WhatsApp, or TUI) and describe the system you want to build:

```
"I want a customer support system with a triage agent and three specialists
for billing, technical issues, and general inquiries."
```

### 3. The Forge takes it from there

It will:
1. Analyze your use case
2. Recommend the right agentic pattern (Routing, in this case)
3. Design your agent roster
4. Generate all workspace files and configuration
5. Validate everything
6. Guide you through deployment

You review and approve at each step. The Forge builds; you decide.

---

## How It Works

The Forge covers the full lifecycle of a multi-agent system through **12 skills** organized into four phases:

```
  DESIGN            ENABLEMENT          HARDENING           PACKAGING
  ──────            ──────────          ─────────           ─────────
  recommend-pattern  equip-agents       harden-workspace    validate-workspace
  design-system      channel-setup      plan-operations     export-package
  add-agent          setup-knowledge                        import-package
                     setup-harness
```

Each skill is a focused capability. You can run them individually or let The Forge chain them together as part of a full system build.

### Session Model

The Forge wakes up fresh each session. It reads its workspace files (SOUL.md, USER.md, recent memory) to restore context. What it learns gets written to memory files so future sessions can pick up where it left off.

### Interaction Model

Every skill follows the same pattern:
1. The Forge analyzes your current state
2. It proposes a plan with rationale
3. You review, adjust, and approve
4. The Forge executes and validates
5. It offers the natural next step

Nothing gets deployed without your sign-off.

---

## Skills Reference

Each skill has a two-letter trigger code. You can invoke skills by trigger or by describing what you need — The Forge recognizes natural language.

### Design Phase

These skills help you architect your agent system from scratch.

#### `recommend-pattern` (RP) — Advisory

**What it does:** Analyzes your use case and recommends the best agentic pattern. Advisory only — no files generated.

**When to use:** You have an idea but aren't sure what architecture fits.

**Say something like:**
- "What pattern should I use for a code review system?"
- "Should I use routing or orchestrator-workers?"
- "Help me choose between these approaches"

**What you get:** Ranked pattern recommendations with trade-off analysis and a conceptual preview of how the system would look in OpenClaw.

**Leads to:** `design-system` (when you're ready to build)

---

#### `design-system` (DS) — Full Build

**What it does:** End-to-end multi-agent system creation. Goes from a natural language description to a complete, deployable OpenClaw workspace.

**When to use:** You're ready to build a new multi-agent system from scratch.

**Say something like:**
- "Build me a research team that can investigate topics in parallel"
- "Create a content pipeline with writer, editor, and fact-checker"
- "Design a multi-agent system for automated code review"

**What you get:**
- Agentic pattern selection with rationale
- Complete agent roster with roles and responsibilities
- Workspace files for every agent (SOUL.md, AGENTS.md, etc.)
- `openclaw.json` configuration with bindings, model config, and tool policies
- Validation report
- Deployment guidance

**Execution flow:**
1. Analyze use case (domain, scale, interaction model)
2. Select pattern (from the 7 proven agentic patterns)
3. Design agent roster (roles, capabilities, relationships)
4. Generate workspace files for each agent
5. Generate `openclaw.json` with all wiring
6. Validate the complete system
7. Offer follow-on skills (equip tools, set up channels, harden)

**Leads to:** `equip-agents`, `channel-setup`, `setup-knowledge`, `harden-workspace`

---

#### `add-agent` (AA) — Extend Existing System

**What it does:** Safely adds one new agent to an existing workspace without breaking what's already running.

**When to use:** You have a working system and want to add a new specialist.

**Say something like:**
- "Add a fact-checker agent to my content pipeline"
- "I need another specialist for handling refunds"
- "Add a monitoring agent that watches for errors"

**What you get:** New agent workspace files, merged configuration, and a validation report confirming the extended system is consistent.

**Execution flow:**
1. Read your existing workspace and config
2. Gather requirements for the new agent
3. Generate workspace artifacts for the new agent
4. Merge config, bindings, and pattern integration
5. Validate the merged system

**Leads to:** `harden-workspace`, `validate-workspace`

---

### Enablement Phase

These skills add infrastructure and tooling to your agent system.

#### `equip-agents` (EA) — Tool Binding

**What it does:** Turns capability statements ("this agent needs to search the web") into concrete tool bindings — MCP servers, APIs, and custom tools.

**When to use:** After designing your system, when agents need real tools to do their work.

**Say something like:**
- "Equip my agents with tools"
- "Find MCP servers for my research team"
- "What tools does each agent need?"

**What you get:**
- Agent-to-tool mapping matrix
- MCP server and API scaffold configurations
- Environment checklist (API keys, connection strings)
- Tool policy suggestions (which tools need approval gates)

**Execution flow:**
1. Load your agent roster
2. Derive tool requirements from each agent's capabilities
3. Research available options (MCP servers first, then APIs, then custom)
4. Present trade-offs and alternatives
5. Confirm selections with you
6. Scaffold configs and stubs
7. Produce a tool plan document

**Leads to:** `channel-setup`, `harden-workspace` (tool policy lockdown)

---

#### `channel-setup` (CS) — Communication Channels

**What it does:** Designs the communication topology for your agent system. Maps each agent to a dedicated channel with categories, naming conventions, and per-channel welcome content. Currently supports Discord.

**When to use:** After your agents are designed and you need to set up where users interact with them.

**Say something like:**
- "Set up Discord channels for my agents"
- "Create a channel layout for my workspace"
- "How should I organize channels for my team?"

**What you get:**
- Categorized channel layout (e.g., Core, Features, Admin)
- Per-channel configuration: name, description, topic, welcome message
- Welcome messages written in each agent's voice with invocation instructions
- Setup checklist for manual creation
- Optional automation script for programmatic channel creation

**Execution flow:**
1. Load agent roster (names, roles, interaction patterns)
2. Select channel platform (Discord currently)
3. Generate channel plan with categories and naming
4. Review and iterate with you
5. Generate per-channel welcome messages and instructions
6. Output complete channel setup document
7. Optionally generate automation script

**Leads to:** `harden-workspace`, `plan-operations`

---

#### `setup-knowledge` (SK) — Memory Architecture

**What it does:** Designs and configures the memory and knowledge architecture for your agent system. Recommends the right tier based on your needs.

**When to use:** When your agents need to remember things across conversations — customer context, research findings, learned patterns.

**Say something like:**
- "Set up memory for my agents"
- "I need a knowledge graph for cross-project learning"
- "My agents should remember customer context"

**Memory tiers:**

| Tier | Backend | Best For |
|------|---------|----------|
| Basic | Flat files (`memory/`) | Session logs, simple context |
| Vector | sqlite-vec / memory_search | Semantic search across past interactions |
| Graph | Neo4j (neo4j-mcp) | Relationship mapping, cross-project patterns |

**What you get:** Memory tier recommendation, backend configuration, capture/recall hooks, and end-to-end verification.

**Leads to:** `harden-workspace`, `validate-workspace`

---

#### `setup-harness` (SH) — Long-Running Resilience

**What it does:** Configures your agents for long-duration tasks that span multiple sessions — checkpointing, heartbeat cadence, session bridging, and resume behavior.

**When to use:** When agents need to work on tasks that take longer than a single session.

**Say something like:**
- "My research agent needs to work across multiple sessions"
- "Set up checkpointing for long tasks"
- "How do I make my agent resume where it left off?"

**What you get:** Heartbeat and compaction settings, progress tracking configuration, session bridging setup, and recovery path verification.

**Leads to:** `harden-workspace`, `validate-workspace`

---

### Hardening & Operations

These skills prepare your system for production use.

#### `harden-workspace` (HW) — Production Hardening

**What it does:** Systematic production-readiness audit and remediation across six dimensions.

**When to use:** When your agents are working and you want them production-grade.

**Say something like:**
- "Harden my workspace"
- "Make my agents production-ready"
- "Security audit my agent system"

**Hardening dimensions:**

| Dimension | What Gets Checked |
|-----------|------------------|
| Memory | Config completeness, retention policies, backup |
| Tool Policies | Least-privilege access, approval gates, safe binary lists |
| Model Failover | Primary + fallback models, timeout config |
| Observability | Heartbeat monitoring, logging, health checks |
| Self-Correction | AGENTS.md guardrails, error recovery instructions |
| Boundaries | SOUL.md constraints, sandbox restrictions |

**What you get:** Before/after comparison with severity-graded findings, applied fixes, and a hardening report.

**Leads to:** `plan-operations`, `validate-workspace`

---

#### `plan-operations` (PO) — Execution Modes

**What it does:** Analyzes your completed system and configures how each agent runs — manually, on a schedule, via webhooks, or with human approval gates.

**When to use:** After hardening, when you're ready to operationalize your system.

**Say something like:**
- "Plan my operations"
- "Set up automation schedules"
- "Which agents should run on cron?"
- "Configure webhooks for my PR reviewer"

**Execution modes:**

| Mode | Fits | OpenClaw Config |
|------|------|----------------|
| Manual | Direct user requests, creative tasks | Channel bindings (default) |
| Cron/Heartbeat | Monitoring, periodic reports, data sync | `cron.enabled`, `heartbeat` settings |
| Webhook | PR reviews, deployment triggers, form submissions | `hooks.enabled`, `hooks.mappings` |
| Human-in-the-loop | Deployments, data modifications, financial ops | `tools.exec.ask`, `approvals.exec` |

**What you get:** Per-agent execution mode classification, complete operations plan, implemented config sections in `openclaw.json`, and validation report.

**Leads to:** `validate-workspace`, `export-package`

---

### Validation & Packaging

These skills verify and distribute your system.

#### `validate-workspace` (VW) — Cross-Artifact Validation

**What it does:** Read-only inspection of your entire workspace. Checks structural integrity, coherence, and hardening completeness.

**When to use:** After any changes, before packaging, or as a periodic health check.

**Say something like:**
- "Validate my workspace"
- "Check if everything is consistent"
- "Is my setup ready for production?"

**What gets checked:**
- All required files exist and have correct structure
- Cross-references resolve (skills reference valid patterns, configs reference valid agents)
- Hardening checklist items are addressed
- No contradictions between workspace files

**What you get:** Categorized findings (CRITICAL / WARNING / INFO), pass/fail verdict, and remediation guidance.

---

#### `export-package` (EP) — Bundle for Sharing

**What it does:** Packages your workspace into a portable `.ocf.zip` file with provenance metadata and setup instructions.

**When to use:** When your system is ready to share or deploy to another OpenClaw instance.

**Say something like:**
- "Export my workspace"
- "Package this for deployment"
- "Create a shareable bundle"

**What you get:** A `.ocf.zip` containing workspace files, skills, config, a `manifest.ocf.json` with version and compatibility info, and a setup prompt for first-run initialization.

---

#### `import-package` (IP) — Install Package

**What it does:** Installs an `.ocf.zip` package into an OpenClaw instance with conflict-aware merging.

**When to use:** When you receive a packaged workspace and want to install it.

**Say something like:**
- "Import this package"
- "Install the workspace bundle"

**What you get:** Installed workspace files, merged configuration (with conflict resolution), integrity verification report, and import event log.

---

## Workspace Files

When The Forge is deployed into OpenClaw, it uses these workspace files:

| File | Purpose | Who Maintains It |
|------|---------|-----------------|
| `SOUL.md` | Personality, principles, boundaries, voice | The Forge evolves it over time |
| `IDENTITY.md` | Identity card — name, creature type, vibe, emoji | Mostly static |
| `AGENTS.md` | Operational playbook — session startup, memory model, tools, safety rules | The Forge adds conventions |
| `TOOLS.md` | MCP server connections and tool-specific operational notes | The Forge fills in at runtime |
| `HEARTBEAT.md` | Proactive check items for heartbeat polls | The Forge updates as needed |
| `USER.md` | Your preferences — communication style, experience level, autonomy settings | You and The Forge together |

### How Sessions Work

Every time The Forge starts a session:

1. Reads `SOUL.md` — remembers who it is
2. Reads `USER.md` — remembers who you are
3. Reads recent `memory/YYYY-MM-DD.md` files — picks up recent context
4. Reads `MEMORY.md` (in main sessions) — loads curated long-term knowledge
5. Loads the pattern library index
6. Checks for active designs in progress

This happens automatically. You just start talking.

### Memory Model

The Forge uses a layered memory system:

- **Daily notes** (`memory/YYYY-MM-DD.md`) — Raw session logs. What happened, what was decided, what patterns were applied.
- **Long-term memory** (`MEMORY.md`) — Curated insights distilled from daily notes. Cross-project lessons, pattern effectiveness ratings, architectural decisions.
- **Knowledge graph** (Neo4j via neo4j-mcp) — Structured relationships: which patterns compose well, what configurations have been validated, how the schema has evolved.
- **Semantic search** (sqlite-vec via memory_search) — Find past designs by use case, pattern, or problem description.

---

## Agentic Patterns

The Forge selects from seven proven patterns based on your use case:

| Pattern | Best For | Example |
|---------|----------|---------|
| **Prompt Chaining** | Sequential processing with quality gates | Content pipeline: draft, edit, fact-check, publish |
| **Routing** | Classifying inputs and directing to specialists | Support system: triage agent routes to billing/tech/general |
| **Parallelization** | Independent subtasks that can run simultaneously | Research: investigate multiple topics at once |
| **Orchestrator-Workers** | Complex tasks with dynamic subtask decomposition | Project manager spawning specialist investigators |
| **Evaluator-Optimizer** | Iterative refinement with quality feedback loops | Code review: write, review, improve, approve |
| **Autonomous Agent** | Open-ended tasks requiring tool use and judgment | Research assistant exploring a topic independently |
| **Long-Running Harness** | Tasks spanning multiple sessions with checkpointing | Multi-day research with progress tracking |

The Forge doesn't just name the pattern — it explains why it fits your use case, what the trade-offs are, and what the OpenClaw implementation looks like.

---

## Examples

### Building a Customer Support System

**You:** "I want a customer support system with a triage agent and three specialists — billing, technical, and general inquiries."

**The Forge:**
1. Analyzes the use case — distinct input categories needing specialist handling
2. Recommends **Routing pattern** — bindings with match rules route to specialists
3. Designs 4 agents: Triage Router, Billing Specialist, Technical Specialist, General Specialist
4. Generates workspace files for each agent
5. Generates `openclaw.json` with bindings, model config, tool policies
6. Offers follow-on: `equip-agents` (bind CRM tools), `channel-setup` (Discord channels), `setup-knowledge` (customer memory)
7. Validates and packages

### Building a Research Team

**You:** "I need a research team that can break down complex topics, investigate in parallel, and synthesize findings."

**The Forge:**
1. Recommends **Orchestrator-Workers pattern** — coordinator spawns specialist workers
2. Designs agents: Research Coordinator + Topic Investigators (spawned dynamically via `sessions_spawn`)
3. Sets up knowledge graph for accumulating findings
4. Configures long-running harness for multi-session research
5. Validates the complete system

### Adding a Fact-Checker to an Existing Pipeline

**You:** "Add a fact-checker agent that reviews everything before it goes to the user."

**The Forge:**
1. Reads your existing workspace
2. Designs the new agent as an **Evaluator-Optimizer** gate
3. Generates its workspace files
4. Merges config — preserving everything that already works
5. Validates the extended system

### Operationalizing a Monitoring System

**You:** "I have a monitoring agent. It should check system health every 15 minutes during business hours and alert via Discord."

**The Forge (plan-operations):**
1. Classifies the agent as **Cron/Heartbeat** execution mode
2. Configures: `heartbeat.every: "15m"`, `heartbeat.activeHours: {start: "09:00", end: "18:00"}`
3. Routes heartbeat output to the monitoring Discord channel
4. Sets up approval gates for any remediation actions
5. Writes config to `openclaw.json`

### Setting Up Discord Channels

**You:** "Set up Discord channels for my 4-agent support system."

**The Forge (channel-setup):**
1. Reads the agent roster
2. Proposes channel layout:
   ```
   SUPPORT
   ├── #triage          → Triage Router
   ├── #billing-support → Billing Specialist
   ├── #tech-support    → Technical Specialist
   └── #general-support → General Specialist

   SYSTEM
   ├── #system-status   → Health and notifications
   └── #admin           → Workspace administration
   ```
3. Generates welcome messages in each agent's voice
4. Produces setup checklist
5. Optionally generates a Discord bot script to create channels programmatically

---

## Build Artifacts

Everything in `dist/` is generated by the Forge Builder (Morgan) and should not be edited by hand.

```
dist/
├── workspace/              # OpenClaw workspace files for The Forge
│   ├── SOUL.md
│   ├── IDENTITY.md
│   ├── AGENTS.md
│   ├── TOOLS.md
│   ├── HEARTBEAT.md
│   └── USER.md
│
├── skills/                 # Skill definitions (one SKILL.md per capability)
│   ├── design-system/          DS
│   ├── add-agent/              AA
│   ├── recommend-pattern/      RP
│   ├── equip-agents/           EA
│   ├── channel-setup/          CS
│   ├── setup-knowledge/        SK
│   ├── setup-harness/          SH
│   ├── harden-workspace/       HW
│   ├── plan-operations/        PO
│   ├── validate-workspace/     VW
│   ├── export-package/         EP
│   └── import-package/         IP
│
├── *.ocf.zip               # Packaged releases
├── RELEASE.md              # Release notes
├── skill-build-context.md  # Build context from last skill generation
└── add-skill-context.md    # Build context from last add-skill run
```

### How Artifacts Are Generated

| Artifact | Workflow | Agent |
|----------|----------|-------|
| `workspace/*` | `build-forge-agent` | Morgan (Forge Builder) |
| `skills/*/SKILL.md` | `build-forge-skill` | Morgan (Forge Builder) |
| `*.ocf.zip` | `package-forge` | Morgan (Forge Builder) |

### Deployment

**Option A — Manual:**
Copy `workspace/` files to your OpenClaw workspace root and `skills/` to the skills directory.

**Option B — Package:**
Use a `.ocf.zip` release with the `import-package` skill for automated installation with conflict-aware merging.

---

## Troubleshooting

### "The Forge doesn't recognize my existing workspace"
- Ensure your OpenClaw workspace has a valid `openclaw.json` at the root
- Check that workspace files are in expected locations

### "Generated config has validation errors"
- Run `update-reference-data` to sync The Forge's config reference with your OpenClaw version
- Then regenerate the config

### "Knowledge graph setup fails"
- Verify MCP server connectivity (neo4j-mcp or memory server)
- Check that the MCP server is available in your OpenClaw instance

### "I'm not sure which skill to use"
- Start with `recommend-pattern` (RP) if you're unsure about architecture
- Use `validate-workspace` (VW) after any changes to catch inconsistencies
- Use `harden-workspace` (HW) before going to production

### Tips

- **Export frequently** — `export-package` creates snapshots you can roll back to
- **Knowledge compounds** — the more your agents interact, the smarter The Forge's recommendations become
- **Let The Forge chain** — after `design-system`, it will naturally suggest `equip-agents`, then `channel-setup`, then `harden-workspace`. Follow the flow.
- **Review, don't rubber-stamp** — The Forge presents everything for your approval. Take the time to understand what it's generating.
