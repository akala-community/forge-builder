# Workflows Reference

forge includes 6 workflows:

---

## build-forge-agent

**Workflow:** `build-forge-agent`

**Purpose:**
Generate The Forge's complete OpenClaw workspace files — SOUL.md, AGENTS.md, IDENTITY.md, and any other required workspace artifacts.

**When to Use:**
When building or rebuilding The Forge's runtime agent from its specification and module brief.

**Key Steps:**
1. Load agent spec and module brief
2. Generate SOUL.md (personality, lore, behavioral guidelines)
3. Generate IDENTITY.md (identity card)
4. Generate AGENTS.md (operational instructions)
5. Generate additional workspace config
6. Validate outputs for consistency

**Agent(s):** Forge Builder (Morgan)

---

## build-forge-skill

**Workflow:** `build-forge-skill`

**Purpose:**
Generate a specific OpenClaw skill's SKILL.md definition and any bundled reference resources it needs at runtime.

**When to Use:**
When building or updating one of The Forge's 9 user-facing skills (design-system, add-agent, recommend-pattern, setup-knowledge, setup-harness, harden-workspace, validate-workspace, export-package, import-package).

**Key Steps:**
1. Select which skill to build
2. Load relevant brief sections and reference data
3. Generate SKILL.md with triggers, flow, and instructions
4. Bundle reference resources
5. Validate skill completeness

**Agent(s):** Forge Builder (Morgan)

---

## add-forge-skill

**Workflow:** `add-forge-skill`

**Purpose:**
Define a new skill for The Forge and register it in the Forge Builder's build pipeline. This is the extensibility workflow that lets The Forge grow new capabilities beyond the initial set.

**When to Use:**
When you want to add a new skill to The Forge that wasn't part of the original design. After adding a skill, run `build-forge-skill` to generate its SKILL.md, then `build-forge-agent` to regenerate The Forge's workspace files with the new capability.

**Key Steps:**
1. Define skill concept (name, purpose, triggers, scope)
2. Load module context (agent specs, existing skills, module brief)
3. Generate skill spec (SKILL.md definition)
4. Register in Forge Builder (add as build-forge-skill target)
5. Update module artifacts (module-help.csv, docs)
6. Validate consistency (naming collisions, trigger conflicts)
7. Prompt rebuild (direct to build-forge-agent)

**Pipeline:** add-forge-skill → build-forge-skill → build-forge-agent

**Agent(s):** Forge Builder (Morgan)

---

## update-reference-data

**Workflow:** `update-reference-data`

**Purpose:**
Refresh the agentic patterns library and OpenClaw configuration reference against the current OpenClaw source code.

**When to Use:**
After OpenClaw updates, to ensure The Forge generates configs that are valid against the latest version.

**Key Steps:**
1. Locate OpenClaw source tree
2. Extract config schema (openclaw.json, bindings, model config)
3. Extract platform features (hooks, spawn config, memory backends)
4. Update pattern library with current feature implementations
5. Write updated config reference
6. Cross-check for accuracy

**Agent(s):** Forge Builder (Morgan)

---

## package-forge

**Workflow:** `package-forge`

**Purpose:**
Bundle The Forge into an installable .ocf.zip package for distribution to OpenClaw users.

**When to Use:**
When The Forge is ready for release — all workspace files, skills, and reference data have been built and validated.

**Key Steps:**
1. Run validate-forge pre-check
2. Collect all artifacts
3. Inject metadata (version, build date, compatibility)
4. Generate setup prompt for first-run
5. Create .ocf.zip archive
6. Verify package integrity

**Agent(s):** Forge Builder (Morgan)

---

## validate-forge

**Workflow:** `validate-forge`

**Purpose:**
Run a comprehensive consistency check across all Forge artifacts to ensure nothing is missing or contradictory.

**When to Use:**
Before packaging, after major changes, or as a periodic health check.

**Key Steps:**
1. Load all workspace files, skills, and reference data
2. Structural checks (required files exist, correct format)
3. Coherence checks (skills reference valid patterns and config)
4. Completeness checks (all 9 skills present with resources)
5. Generate validation report

**Agent(s):** Forge Builder (Morgan)
