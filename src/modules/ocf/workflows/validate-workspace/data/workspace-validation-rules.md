# Workspace Validation Rules

This document defines all validation rules used by the validate-workspace workflow. Rules are organized by category (structural, coherence, hardening) and each rule specifies its ID, description, severity, and check procedure.

---

## Severity Levels

| Level | Meaning |
|-------|---------|
| **ERROR** | Critical issue. The workspace is broken or non-functional. Contributes to FAIL status. |
| **WARNING** | Non-critical issue. The workspace functions but is missing recommended configuration. Contributes to WARNINGS status. |
| **INFO** | Informational note. No impact on pass/fail status. |

---

## Category 1: Structural Checks

Structural checks verify that the workspace has all required files, expected files, and proper directory structure.

### S-01: Required File Presence

| Rule | Description |
|------|-------------|
| **ID** | S-01 |
| **Severity** | ERROR (per missing file) |
| **Description** | All required workspace files must be present |
| **Check** | Verify each of the following files exists in the workspace root |

**Required files:**

| File | Purpose |
|------|---------|
| `AGENTS.md` | Main agent directives -- startup instructions, tool/skill bindings, session management |
| `SOUL.md` | Personality definition, identity, communication style, boundaries |
| `USER.md` | User preferences, context, interaction patterns |
| `IDENTITY.md` | Agent name, emoji, avatar, theme configuration |
| `TOOLS.md` | Tool usage guidance, policies, access rules |
| `HEARTBEAT.md` | Heartbeat/cron configuration for periodic tasks |
| `MEMORY.md` | Memory handling directives and backend configuration |
| `BOOT.md` | Bootstrap sequence and initialization instructions |

### S-02: File Non-Empty Check

| Rule | Description |
|------|-------------|
| **ID** | S-02 |
| **Severity** | ERROR (per empty required file), WARNING (per empty optional file) |
| **Description** | All present files must contain content (non-empty) |
| **Check** | For each file found, verify it is not empty (has more than whitespace) |

### S-03: File Well-Formedness

| Rule | Description |
|------|-------------|
| **ID** | S-03 |
| **Severity** | WARNING |
| **Description** | Files with YAML frontmatter should have valid frontmatter blocks |
| **Check** | If a file starts with `---`, verify the frontmatter block closes with a second `---` and contains valid YAML |

### S-04: Directory Structure

| Rule | Description |
|------|-------------|
| **ID** | S-04 |
| **Severity** | WARNING (per missing directory) |
| **Description** | Expected directories should exist |
| **Check** | Verify the following directories exist in the workspace |

**Expected directories:**

| Directory | Purpose |
|-----------|---------|
| `memory/` | Memory state files, persistent storage |
| `skills/` | Skill definition files |

### S-05: BOOTSTRAP.md Absence

| Rule | Description |
|------|-------------|
| **ID** | S-05 |
| **Severity** | WARNING |
| **Description** | BOOTSTRAP.md should NOT be present after initial bootstrap is complete |
| **Check** | Verify `BOOTSTRAP.md` does NOT exist in the workspace root. If present, it indicates the bootstrap workflow was not finalized or cleanup was skipped. |

### S-06: openclaw.json Presence

| Rule | Description |
|------|-------------|
| **ID** | S-06 |
| **Severity** | WARNING |
| **Description** | openclaw.json configuration file should exist |
| **Check** | Verify `openclaw.json` exists in the workspace root. If present, verify it is valid JSON. |

---

## Category 2: Coherence Checks

Coherence checks verify cross-artifact consistency -- that references between files are valid and content is aligned.

### C-01: SOUL.md and AGENTS.md Personality Consistency

| Rule | Description |
|------|-------------|
| **ID** | C-01 |
| **Severity** | WARNING |
| **Description** | SOUL.md personality should be referenced or reflected in AGENTS.md |
| **Check** | Read SOUL.md to extract the agent name and key personality traits. Read AGENTS.md and verify it references SOUL.md in its startup/initialization sequence. The agent name used in AGENTS.md should match or reference the name defined in SOUL.md. |

### C-02: AGENTS.md Session Startup References

| Rule | Description |
|------|-------------|
| **ID** | C-02 |
| **Severity** | WARNING |
| **Description** | AGENTS.md should reference other workspace files in its startup sequence |
| **Check** | Read AGENTS.md and verify it contains references to the following files in its startup or initialization instructions: SOUL.md, USER.md, MEMORY.md (or memory-related directives). Missing references indicate the agent may not load all workspace context on startup. |

### C-03: Skill References vs Actual Skills

| Rule | Description |
|------|-------------|
| **ID** | C-03 |
| **Severity** | WARNING (per orphaned or missing skill) |
| **Description** | Skills referenced in AGENTS.md should match actual skill files |
| **Check** | Extract skill references from AGENTS.md (look for skill bindings, skill lists, or references to files in skills/). List all .md files in the skills/ directory. Report: (a) skills referenced in AGENTS.md but missing from skills/ directory, (b) skill files present in skills/ but not referenced in AGENTS.md. |

### C-04: openclaw.json Binding Completeness

| Rule | Description |
|------|-------------|
| **ID** | C-04 |
| **Severity** | WARNING |
| **Description** | If openclaw.json exists, its agent and binding entries should be consistent |
| **Check** | If openclaw.json exists, verify: (a) agents listed in agents.list have valid workspace paths, (b) bindings reference agents that exist in agents.list, (c) channel references in bindings point to channels defined in channels section. |

### C-05: IDENTITY.md Consistency with SOUL.md

| Rule | Description |
|------|-------------|
| **ID** | C-05 |
| **Severity** | WARNING |
| **Description** | Agent name and identity in IDENTITY.md should be consistent with SOUL.md |
| **Check** | If both IDENTITY.md and SOUL.md exist, read both files. Verify the agent name referenced in IDENTITY.md matches the name defined in SOUL.md. Flag discrepancies where the identity appears to describe a different agent. |

---

## Category 3: Hardening Checks

Hardening checks verify security, resilience, and operational production-readiness.

### H-01: Memory Directives in AGENTS.md

| Rule | Description |
|------|-------------|
| **ID** | H-01 |
| **Severity** | WARNING |
| **Description** | AGENTS.md should contain memory-related directives |
| **Check** | Read AGENTS.md and check for the presence of memory-related sections or directives. Look for keywords: memory, remember, recall, persist, save, store. A production agent should have explicit instructions about when and how to use memory. |

### H-02: Memory Backend Configuration

| Rule | Description |
|------|-------------|
| **ID** | H-02 |
| **Severity** | INFO (if no openclaw.json), WARNING (if openclaw.json exists but memorySearch is missing or disabled) |
| **Description** | Memory backend should be configured in openclaw.json |
| **Check** | If openclaw.json exists, check for `memorySearch` configuration block. Verify: (a) `memorySearch.enabled` is true, (b) `memorySearch.provider` is set, (c) `memorySearch.store` is set. |

### H-03: Tool Policies

| Rule | Description |
|------|-------------|
| **ID** | H-03 |
| **Severity** | INFO (if no openclaw.json), WARNING (if openclaw.json exists but tools config is minimal) |
| **Description** | Tool policies should be configured for production use |
| **Check** | If openclaw.json exists, check for `tools` configuration block. Verify: (a) `tools.profile` is set (one of: "minimal", "coding", "messaging", "full"), (b) review `tools.allow` and `tools.deny` arrays if present, (c) check `tools.exec` and `tools.web` settings. Report the configured profile and any explicit allow/deny rules. |

### H-04: Boundaries in SOUL.md

| Rule | Description |
|------|-------------|
| **ID** | H-04 |
| **Severity** | WARNING |
| **Description** | SOUL.md should define operational boundaries |
| **Check** | Read SOUL.md and look for a boundaries section or explicit boundary-related directives. Look for keywords: boundary, boundaries, limit, forbidden, never, must not, off-limits, scope. A production agent should have clearly defined boundaries for what it will and will not do. |

### H-05: Failover Configuration

| Rule | Description |
|------|-------------|
| **ID** | H-05 |
| **Severity** | INFO (if no openclaw.json), WARNING (if openclaw.json exists but no failover) |
| **Description** | Model failover chain should be configured for resilience |
| **Check** | If openclaw.json exists, check for `model` configuration block. Verify: (a) `model.primary` is set, (b) `model.fallbacks` is set and contains at least one fallback model. An agent without failover will fail completely if the primary model is unavailable. |

### H-06: Compaction Configuration

| Rule | Description |
|------|-------------|
| **ID** | H-06 |
| **Severity** | INFO |
| **Description** | Compaction settings should be reviewed for production suitability |
| **Check** | If openclaw.json exists, check for `compaction` configuration block. Report: (a) `compaction.mode` value ("default" or "safeguard"), (b) `compaction.maxHistoryShare` value, (c) `compaction.memoryFlush` value. If mode is "default", note that "safeguard" mode provides better memory preservation. |

### H-07: Safety Section in AGENTS.md

| Rule | Description |
|------|-------------|
| **ID** | H-07 |
| **Severity** | WARNING |
| **Description** | AGENTS.md should contain a safety or guardrails section |
| **Check** | Read AGENTS.md and look for safety-related sections or directives. Look for keywords: safety, guardrail, guard, protect, caution, danger, harm, risk, ethics, responsible. A production agent should have explicit safety guidelines. |

---

## Overall Status Calculation

| Condition | Overall Status |
|-----------|---------------|
| Zero ERRORs and zero WARNINGs | **PASS** |
| Zero ERRORs but one or more WARNINGs | **WARNINGS** |
| One or more ERRORs (regardless of WARNINGs) | **FAIL** |
