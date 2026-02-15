---
selectedSkill: 'import-package'
skillCategory: 'utility'
stepsCompleted: ['step-01-select-skill', 'step-02-load-context', 'step-03-generate-skill']
date: '2026-02-14'
---

# Skill Build: import-package

## Selected Skill

**Name:** import-package
**Category:** Utility
**Purpose:** Install workspace package
**Triggers:** "import", "install package"
**Flow:** Receive .ocf.zip -> Validate contents -> Install files -> Merge config -> Verify
**Data Needs:** Package validation rules, merge conflict resolution logic
**Complexity:** Medium — merge handling

---

## Loaded Context

### Module Brief Extract

**Executive Summary:**
The Forge is a meta-agent — an AI agent that designs, builds, configures, and deploys other AI agent systems. It lives inside OpenClaw as a native agent, accessible through any channel (WhatsApp, Telegram, Discord, TUI). Users describe what they need in natural language and The Forge generates a production-ready, multi-agent deployment.

**import-package Skill Row (Utility):**

| Skill | Trigger Examples | Purpose | Flow |
|-------|-----------------|---------|------|
| `import-package` | "import", "install package" | Install workspace package | Receive .ocf.zip -> Validate contents -> Install files -> Merge config -> Verify |

**Agent Architecture:**
- Single OpenClaw runtime agent (The Forge) with multiple skills
- Skill-based capability switching
- For complex tasks, uses OpenClaw's `sessions_spawn` to parallelize — Orchestrator-Workers pattern
- Uses OpenClaw's memory system for cross-session continuity

**Communication Style:**
Precise yet approachable. Master craftsman who uses forge metaphors naturally:
- Designing agents = "forging"
- Configuration = "tempering"
- Validation = "quality inspection"
- Completed system = "a blade leaving the forge"
- Hardening = metallurgy term — fits naturally
- Knowledge graph = "the memory anvil"
- Patterns = "blueprints"

Voice during import-package: Receiving and installing — "Let me inspect this piece and find it a proper home in your forge."

**The Builder's Journey (primary persona for import-package):**
1. Receives a .ocf.zip package from a teammate or community
2. "Import this package" — The Forge receives the file
3. Validates the package contents (structural integrity, manifest, compatibility)
4. Installs workspace files into the correct locations
5. Merges config (openclaw.json bindings, model settings) with existing setup
6. Runs validation to verify the imported system works alongside existing agents
7. User has a new agent system running alongside their existing setup

**The Scaler's Journey (secondary persona for import-package):**
1. Already has agents running, wants to add a pre-built system
2. "Install this customer support package" — The Forge handles merge conflicts
3. Config merging resolves binding conflicts, model fallback chains, tool policy overlaps
4. Validation confirms no regressions to existing agents

**Tools & Integrations Relevant to import-package:**

| Feature | How Used |
|---------|----------|
| `memory/` daily logs | Record import events, track what was installed and from where |
| Compaction (safeguard mode) | Context management if package is large |
| File system access | Read .ocf.zip contents, write workspace files to correct paths |

**Workflow Connections:**
```
export-package ----> import-package (recipient installs the package)
import-package ----> validate-workspace (verify after import)
```

**Unique Value Proposition — Import:**
- **Merge intelligence** — doesn't blindly overwrite; merges config with conflict detection and resolution
- **Validation after install** — automatically chains to validate-workspace to confirm nothing broke
- **Provenance tracking** — records who built the package, when, and what patterns it uses
- **Forge-native metaphor** — "Let me inspect this piece and find it a proper home in your forge"

### Skill Registry Details

- **Category:** Utility
- **Trigger Examples:** "import", "install package"
- **Purpose:** Install workspace package
- **Flow:** Receive .ocf.zip -> Validate contents -> Install files -> Merge config -> Verify
- **Data Needs:** Package validation rules, merge conflict resolution logic
- **Complexity:** Medium — merge handling
- **Connections:** export-package --> import-package, import-package --> validate-workspace

### Agentic Patterns

N/A — import-package does not directly implement an agentic pattern. It is an installation/merge utility skill. However, it must understand workspace structures produced by all patterns so it can correctly install and merge them:

| Pattern | Import Considerations |
|---------|----------------------|
| Prompt Chaining | Install sequential agent workspace files, preserve ordering in config |
| Routing | Merge specialist agent bindings without conflicting with existing routes |
| Parallelization | Merge concurrent agent configs + maxConcurrent settings |
| Orchestrator-Workers | Install parent + all worker agent workspaces, preserve spawn relationships |
| Evaluator-Optimizer | Install reviewer agent config + critique loop settings |
| Autonomous Agent | Merge tool policies without weakening existing sandbox boundaries |
| Long-Running Harness | Install checkpoint config + progress persistence setup |

### Context Summary

**Key inputs for SKILL.md generation:**
- Trigger examples: 2 examples loaded ("import", "install package")
- Flow steps: 5 steps defined (Receive .ocf.zip -> Validate contents -> Install files -> Merge config -> Verify)
- Data needs: Package validation rules, merge conflict resolution logic
- Related skills: export-package (upstream), validate-workspace (downstream)

---

## Generation Complete

**SKILL.md written to:** _bmad-output/forge-artifacts/skills/import-package/SKILL.md
**Sections generated:** Triggers, Execution Flow, Instructions, Data Dependencies, Connected Skills, Success Criteria
**User confirmed:** Yes
