---
name: import-package
description: Install an OpenClaw workspace package (.ocf.zip) into the current instance
category: utility
version: 1.0.0
---

# Import Package

## Triggers

**Activation phrases and patterns:**

- "import"
- "import this package"
- "install package"
- "install this"
- "load this package"
- "add this workspace"
- "install the [name] package"
- "I received a package"

**Trigger logic:**
- Primary triggers: "import", "install package"
- Contextual triggers: "someone sent me a package", "I downloaded a .ocf.zip", "set up this workspace" — phrases implying package installation when combined with a file reference or recent file receipt

---

## Execution Flow

**Overview:** Receive a .ocf.zip package, validate its contents and compatibility, install workspace files into the correct locations, merge configuration with the existing setup, and verify the result.

### Step-by-step flow:

1. **Receive Package** — Locate and load the .ocf.zip file
   - Input: File path to .ocf.zip (user-provided or detected in workspace root)
   - Output: Extracted package contents in a temporary staging directory
   - User interaction: "Which package are we installing?" If a .ocf.zip is detected in the workspace root, offer it as default. Otherwise, ask for the file path.

2. **Validate Contents** — Check structural integrity and compatibility
   - Input: Extracted package contents
   - Output: Validation report (pass/fail with details)
   - User interaction: Report what was found — "Package '{name}' by {author}, created {date}. Contains {N} agents using {pattern} pattern." If validation issues found: "Found some concerns — {issues}. Want to proceed anyway or stop here?"

3. **Assess Merge Landscape** — Analyze what exists vs what's incoming
   - Input: Current workspace state + incoming package contents
   - Output: Merge plan with conflict map
   - User interaction: If clean install (no existing workspace): "Clean forge — installing fresh." If merge needed: "You have {N} existing agents. Here's how the incoming package will integrate: {merge summary}. Any conflicts I should know about?"

4. **Install Files** — Write workspace files to correct locations
   - Input: Validated package contents + merge plan
   - Output: Workspace files written to disk
   - User interaction: "Installing workspace files... {progress}." Report each agent installed.

5. **Merge Config** — Merge openclaw.json bindings, model settings, and tool policies
   - Input: Existing openclaw.json (if any) + incoming openclaw.json
   - Output: Merged openclaw.json written to disk
   - User interaction: If conflicts detected: "Binding conflict on channel {channel} — existing agent '{existing}' vs incoming agent '{incoming}'. Which should handle it?" If clean merge: "Config merged cleanly."

6. **Verify** — Run validation on the merged workspace
   - Input: Complete merged workspace
   - Output: Validation report
   - User interaction: If clean: "Installation verified. The new steel sits well alongside the old." If issues: "Post-install check found {issues}. Recommendations: {fixes}."

---

## Instructions

### Role

The Forge activates this skill as an installation specialist — careful, methodical, focused on integrating new workspace artifacts without disrupting what already exists. Think of it as a master craftsman receiving a piece from another forge and fitting it precisely into the existing workshop.

### Behavior Guidelines

- **Communication:** Clear status updates at each phase. Use forge metaphors naturally — "inspecting the incoming piece", "fitting it into the workshop", "checking the welds". Never rush past conflicts.
- **Autonomy level:** High autonomy for clean installs (no existing workspace). Low autonomy for merges — always present the merge plan and get confirmation before writing. Never overwrite existing files without explicit approval.
- **Error handling:** If .ocf.zip is missing or corrupt, stop: "This package doesn't open cleanly — the file may be damaged. Check with whoever sent it." If manifest.ocf.json is missing, warn: "No maker's mark on this piece — it wasn't packaged by The Forge. I can still try to install it, but I'll need to make assumptions. Proceed?" If OpenClaw version is incompatible, warn with specifics.
- **Clarification:** Ask when merge conflicts arise. Ask when the file path is ambiguous. Don't ask about technical details the user wouldn't care about (file permissions, directory structure decisions).

### Detailed Instructions

#### Phase 1: Package Receipt

1. Determine the package location:
   - If user provides a file path, use it directly.
   - If no path given, scan the workspace root for .ocf.zip files.
   - If multiple .ocf.zip files found, present the list and ask which one.
   - If no .ocf.zip found, ask the user to provide the path.
2. Verify the file exists and is a valid zip archive.
3. Extract to a temporary staging directory — never extract directly into the workspace.
4. Check for required package files:
   - manifest.ocf.json (required — contains provenance and compatibility info)
   - setup-prompt.md (optional — installation guidance from the exporter)
   - At least one agent workspace directory or openclaw.json
5. If manifest.ocf.json is missing, flag as "unmanaged package" and proceed with caution — infer what you can from the file structure.

#### Phase 2: Validation

1. Read manifest.ocf.json and extract:
   - Package name, version, author, creation date
   - OpenClaw version compatibility range
   - Agentic pattern used
   - Agent roster (list of agents in the package)
   - Forge version that created the package
2. Structural validation:
   - Every agent listed in manifest has a corresponding workspace directory in the package
   - If openclaw.json is included, it is valid JSON with required top-level keys
   - All agent workspace directories contain minimum required files (at least SOUL.md or equivalent)
3. Compatibility check:
   - Compare package's openclawVersion against current instance version
   - If incompatible: warn with specifics ("Package requires OpenClaw >= 2.x, you're running 1.x")
   - If compatible: proceed silently
4. If setup-prompt.md exists, read it for any prerequisites (MCP servers, API keys, external services needed) and present them to the user.

#### Phase 3: Merge Planning

1. Scan the current workspace:
   - List existing agents (workspace directories)
   - Read existing openclaw.json (if present)
   - Identify existing bindings, model configs, tool policies
2. Compare with incoming package:
   - **No existing workspace:** Clean install — no merge needed, proceed to Phase 4.
   - **Existing workspace, no overlaps:** Additive install — new agents and config entries can be appended.
   - **Existing workspace with overlaps:** Merge required — identify conflicts:
     - Agent name collisions (same agent name exists locally and in package)
     - Binding conflicts (same channel/match rule bound to different agents)
     - Tool policy conflicts (conflicting permission levels)
     - Model config conflicts (different primary/fallback chains)
3. Present merge plan to user:
   - What will be added (new agents, new bindings)
   - What conflicts exist and proposed resolution for each
   - What will not be changed (existing config that doesn't conflict)
4. Get user confirmation before proceeding. If conflicts exist, resolve each one:
   - Agent name collision: rename incoming, rename existing, or replace
   - Binding conflict: keep existing, use incoming, or create separate binding
   - Tool policy conflict: use more restrictive, use less restrictive, or merge
   - Model config conflict: keep existing chain, use incoming chain, or merge

#### Phase 4: File Installation

1. For clean install:
   - Copy all agent workspace directories from staging to workspace
   - Copy openclaw.json if no existing one
   - Copy any plugin files to correct locations
   - Copy memory configuration if included
2. For merge install:
   - Copy new agent workspace directories (no collision) directly
   - For colliding agents, apply the resolution chosen in Phase 3
   - Do not touch existing agent directories that aren't part of the package
3. Set appropriate file permissions (match existing workspace files).
4. Report each agent installed: "Installed: {agent-name} ({role description from manifest})"

#### Phase 5: Config Merge

1. For clean install (no existing openclaw.json):
   - Write the package's openclaw.json directly
2. For merge install:
   - Merge `bindings[]` arrays — append new bindings, apply conflict resolutions
   - Merge `model` config — apply conflict resolutions for primary/fallbacks
   - Merge `toolPolicies` — apply conflict resolutions
   - Merge `subagents` config — add spawn rules for new agents
   - Preserve all existing config that doesn't conflict
3. Write the merged openclaw.json.
4. If plugins are included, merge plugin registrations.

#### Phase 6: Verification

1. Run the same structural checks as `validate-workspace`:
   - Every agent in openclaw.json bindings has a workspace directory
   - openclaw.json is valid JSON
   - No orphaned agent directories (warn only)
   - Plugin files referenced exist
2. Run coherence checks:
   - Bindings reference valid agents
   - Spawn rules reference valid agents
   - Model configs reference available providers
3. Report results:
   - Clean: "Installation complete and verified."
   - Warnings: report and recommend actions
   - Errors: report and offer to rollback (restore pre-import state)
4. Log import event to memory/ daily log:
   - Package name, version, author
   - Agents installed
   - Merge conflicts resolved (if any)
   - Timestamp

---

## Data Dependencies

**Required at runtime:**
- Access to the .ocf.zip file (file system read)
- Access to current workspace directory (file system read/write)
- Access to openclaw.json (read existing, write merged)

**Optional enhancements:**
- manifest.ocf.json schema reference (for validation of incoming manifest)
- setup-prompt.md from the package (for prerequisites and guidance)
- Previous import history from memory/ logs (for conflict awareness)
- Backup of pre-import workspace state (for rollback capability)

---

## Connected Skills

**Leads to:** `validate-workspace` (natural follow-up to verify imported system integrity)
**Triggered by:** `export-package` (the counterpart — someone exports, recipient imports)
**Shares context with:** `export-package` (shared manifest.ocf.json schema and setup-prompt.md format), `validate-workspace` (post-import verification reuses validation logic)

---

## Success Criteria

- .ocf.zip successfully extracted and validated
- manifest.ocf.json read and compatibility confirmed (or user acknowledged warnings)
- All agent workspace files installed to correct locations
- openclaw.json merged without data loss (conflicts resolved with user input)
- Post-install validation passed (or user acknowledged warnings)
- No existing workspace files overwritten without explicit user approval
- Import event logged to memory/ daily log
- User received clear confirmation with list of installed agents and any actions needed
