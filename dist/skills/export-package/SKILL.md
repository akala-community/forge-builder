---
name: export-package
description: Bundle workspace for sharing as a portable .ocf.zip package
category: utility
version: 1.0.0
---

# Export Package

## Triggers

**Activation phrases and patterns:**

- "export"
- "export my setup"
- "package"
- "package this"
- "share my setup"
- "bundle my workspace"
- "create a package"
- "make this portable"
- "send my config to someone"

**Trigger logic:**
- Primary triggers: "export", "package", "share my setup"
- Contextual triggers: "send this to [person]", "make a template from this", "I want to share my agents" — phrases implying workspace portability when combined with workspace context

---

## Execution Flow

**Overview:** Load the current workspace, inject provenance metadata, generate an AI-readable setup prompt, and bundle everything into a portable .ocf.zip package.

### Step-by-step flow:

1. **Load Workspace** — Discover and read all workspace artifacts
   - Input: Current OpenClaw workspace directory
   - Output: Complete inventory of workspace files (agent workspace files, openclaw.json, plugins, memory config, hooks)
   - User interaction: "Let me take stock of what we're packaging." Report what was found — agent count, config presence, plugins, memory setup.

2. **Validate Before Export** — Run a lightweight structural check
   - Input: Loaded workspace inventory
   - Output: Validation pass/fail with any warnings
   - User interaction: If issues found: "Found a few rough edges — {issues}. Want to fix these before packaging, or export as-is?" If clean: "Everything checks out. Clean steel."

3. **Inject Metadata** — Add provenance and package metadata
   - Input: Validated workspace, current date, user identity, OpenClaw version
   - Output: Package manifest (manifest.ocf.json) with: package name, version, author, creation date, agentic pattern used, agent roster, OpenClaw version compatibility, description
   - User interaction: "What should we call this package?" Prompt for package name and optional description. Suggest defaults based on workspace content.

4. **Generate Setup Prompt** — Create an AI-readable installation guide
   - Input: Workspace structure, manifest, agent configurations
   - Output: setup-prompt.md — a markdown document that guides the `import-package` skill (or a human) through installing and configuring the package in a new OpenClaw instance
   - User interaction: "I've drafted a setup guide that will travel with the package. Want to review it?"

5. **Bundle .ocf.zip** — Assemble the final portable package
   - Input: All workspace files + manifest.ocf.json + setup-prompt.md
   - Output: {package-name}.ocf.zip written to the workspace root
   - User interaction: "Another fine piece leaves the forge. Package ready at: {path}. {file size}, {agent count} agents, ready to travel."

---

## Instructions

### Role

The Forge activates this skill as a packaging specialist — methodical, thorough, focused on producing a portable artifact that faithfully reproduces the workspace elsewhere. Think of it as a master craftsman carefully wrapping a finished blade for delivery.

### Behavior Guidelines

- **Communication:** Concise status updates at each step. Use forge metaphors naturally — "wrapping the blade", "stamping the maker's mark" (metadata), "another piece leaves the forge."
- **Autonomy level:** High autonomy for discovery and bundling. Pause for user input on package name, description, and whether to fix validation issues.
- **Error handling:** If workspace is empty or has no agents defined, stop and explain: "Nothing in the forge to package. Build or import a workspace first." If critical files are missing (no openclaw.json), warn and ask whether to proceed.
- **Clarification:** Ask when the package name/description is ambiguous. Don't ask about technical details the user wouldn't know (zip compression level, file ordering).

### Detailed Instructions

#### Phase 1: Discovery

1. Read the current workspace directory structure.
2. Identify all workspace artifact types present:
   - Agent workspace files (SOUL.md, AGENTS.md, IDENTITY.md, etc.) per agent subdirectory
   - openclaw.json (main config with bindings, model config, tool policies)
   - Plugin files (if any — e.g., knowledge-graph extension)
   - Memory configuration (memory/ directory structure, memorySearch config)
   - Hook definitions (before_agent_start, agent_end, etc.)
   - Custom skill files (SKILL.md files in skills/ directories)
3. Build a workspace inventory: list of files, categorized by type.
4. Report the inventory to the user with counts: "{N} agents, {M} plugins, {K} skills found."
5. If inventory is empty (no agents, no config), halt: "The forge is cold — no workspace to package. Use `design-system` to build one first."

#### Phase 2: Pre-Export Validation

1. Run lightweight structural checks:
   - Every agent referenced in openclaw.json bindings has a corresponding workspace directory
   - openclaw.json is valid JSON and has required top-level keys
   - No orphaned agent directories (workspace dirs with no binding reference) — warn but don't block
   - Plugin files referenced in config exist on disk
2. Report findings:
   - Clean: proceed silently
   - Warnings: report and ask "Fix or export as-is?"
   - Errors: report and recommend fixing before export

#### Phase 3: Metadata Injection

1. Prompt user for:
   - Package name (suggest default from workspace name or primary agent name)
   - Package description (optional — suggest default from workspace purpose)
2. Auto-populate manifest.ocf.json:
   - `name`: user-provided or default
   - `version`: "1.0.0" (first export) or increment if re-exporting
   - `author`: from OpenClaw user config or prompt
   - `createdAt`: current ISO timestamp
   - `openclawVersion`: current OpenClaw version for compatibility
   - `agenticPattern`: detected pattern from workspace config (if identifiable)
   - `agents`: list of agent names from workspace
   - `description`: user-provided or auto-generated summary
   - `forge_version`: The Forge version that created this package

#### Phase 4: Setup Prompt Generation

1. Generate setup-prompt.md containing:
   - Package overview (what this workspace does)
   - Prerequisites (OpenClaw version, required MCP servers, external services)
   - Installation steps for `import-package` skill
   - Manual installation steps (for users without The Forge)
   - Agent roster description (what each agent does)
   - Post-install configuration notes (API keys, channel bindings, etc.)
   - Verification steps (how to confirm it's working)
2. Present setup-prompt.md to user for optional review.
3. Incorporate any feedback.

#### Phase 5: Bundling

1. Create a temporary staging directory.
2. Copy all workspace files maintaining directory structure.
3. Add manifest.ocf.json at package root.
4. Add setup-prompt.md at package root.
5. Compress into {package-name}.ocf.zip.
6. Write to workspace root directory.
7. Report: package path, file size, contents summary.
8. Log export event to memory/ daily log.

---

## Data Dependencies

**Required at runtime:**
- Access to current workspace directory (file system read)
- Access to openclaw.json configuration
- File system write access for .ocf.zip output

**Optional enhancements:**
- Package manifest template (manifest.ocf.json schema reference)
- Setup prompt template (boilerplate structure for setup-prompt.md)
- Previous export history from memory/ logs (for version incrementing)
- OpenClaw version info (for compatibility stamping)

---

## Connected Skills

**Leads to:** `import-package` (recipient uses this to install the exported package)
**Triggered by:** `design-system` (natural follow-up after building a system), `harden-workspace` (export after hardening), `validate-workspace` (export after validation confirms quality)
**Shares context with:** `validate-workspace` (pre-export validation reuses validation logic), `import-package` (shared manifest.ocf.json schema and setup-prompt.md format)

---

## Success Criteria

- All workspace files discovered and included in the package
- Pre-export validation passed (or user acknowledged warnings)
- manifest.ocf.json contains accurate provenance metadata
- setup-prompt.md provides clear, complete installation guidance
- .ocf.zip is a valid archive that can be unzipped and installed via `import-package`
- Package file written to the expected location
- Export event logged to memory/ daily log
- User received clear confirmation with package path and summary
