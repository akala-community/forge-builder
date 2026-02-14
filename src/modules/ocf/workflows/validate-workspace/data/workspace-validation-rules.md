# Workspace Validation Rules

Reference data for the validate-workspace workflow. These rules define what constitutes a valid, consistent, and hardened OpenClaw workspace.

---

## Structural Checks

### Required Files (FAIL if missing)

| File | Severity | Rule |
|------|----------|------|
| SOUL.md | FAIL | Must exist and be non-empty. Defines agent personality and boundaries. Required sections: ## Core Truths, ## Boundaries, ## Vibe, ## Continuity. |
| AGENTS.md | FAIL | Must exist and be non-empty. Defines agent operational procedures. Must reference SOUL.md, USER.md, memory/. |
| USER.md | FAIL | Must exist. Defines the user the agent serves. Expected fields: Name, Pronouns, Timezone, Notes, ## Context. |

### Expected Files (WARN if missing)

| File | Severity | Rule |
|------|----------|------|
| IDENTITY.md | WARN | Should exist. Defines agent name, creature, vibe, emoji, and avatar. If absent, check SOUL.md for identity section. |
| TOOLS.md | WARN | Should exist if agent uses tools. User-maintained local tool configuration notes. |
| HEARTBEAT.md | WARN | Should exist if heartbeat is configured. Periodic task checklist. |

### Optional Files (INFO if missing)

| File | Severity | Rule |
|------|----------|------|
| MEMORY.md | WARN | Should exist if memory backend is enabled. Curated long-term memory (free-form, no required structure). |
| BOOT.md | WARN | Should exist. Startup instructions read every session. |

### Files That Should NOT Exist (anti-patterns)

| File | Severity | Rule |
|------|----------|------|
| BOOTSTRAP.md | WARN | Should NOT exist in a fully initialized workspace. First-run script that should be deleted after setup. |

### Required Directories

| Directory | Severity | Rule |
|-----------|----------|------|
| memory/ | WARN | Should exist for daily notes (memory/YYYY-MM-DD.md). |

### Optional Directories

| Directory | Severity | Rule |
|-----------|----------|------|
| skills/ | WARN | Should exist if AGENTS.md or TOOLS.md references skills. Each skill is a subdirectory. |

### Skill Well-Formedness

| Check | Severity | Rule |
|-------|----------|------|
| SKILL.md exists per skill directory | FAIL | Each skill subdirectory under skills/ must contain a SKILL.md file. |
| SKILL.md has name frontmatter | WARN | SKILL.md must have YAML frontmatter with a `name` field. |
| SKILL.md has description frontmatter | WARN | SKILL.md must have YAML frontmatter with a `description` field. |
| SKILL.md has ONLY name+description frontmatter | INFO | SKILL.md frontmatter should contain only `name` and `description` fields -- no other configuration. |

### File Well-Formedness

| Check | Severity | Rule |
|-------|----------|------|
| SOUL.md has ## sections | WARN | Should have structured sections: ## Core Truths, ## Boundaries, ## Vibe, ## Continuity. |
| AGENTS.md has ## sections | WARN | Should have structured sections covering: Every Session, Memory, Safety, Tools. |
| USER.md has content | WARN | Should contain at minimum the user's name or preferences (Name, Pronouns, Timezone, Notes, ## Context). |
| IDENTITY.md has content | WARN | Should contain identity fields (Name, Creature, Vibe, Emoji, Avatar). |
| HEARTBEAT.md has checklist | WARN | Should contain a periodic task checklist. |

---

## Coherence Checks

### AGENTS.md References

| Check | Severity | Rule |
|-------|----------|------|
| AGENTS.md references SOUL.md | FAIL | Session startup must instruct agent to read SOUL.md. Verify SOUL.md exists. |
| AGENTS.md references USER.md | FAIL | Session startup must instruct agent to read USER.md. Verify USER.md exists. |
| AGENTS.md references memory/ | FAIL | Session startup must instruct agent to read memory/YYYY-MM-DD.md or equivalent daily notes. Verify memory/ directory exists. |
| AGENTS.md references MEMORY.md | WARN | Should instruct agent to read MEMORY.md in main sessions. |

### Personality-Directive Consistency

| Check | Severity | Rule |
|-------|----------|------|
| SOUL.md has Boundaries section | FAIL | Boundaries section must be present and non-empty. |
| SOUL.md tone is consistent | WARN | The personality tone in SOUL.md should not contradict AGENTS.md directives. Check for conflicting instructions (e.g., "be bold" in SOUL vs "always ask permission" in AGENTS). |

### Identity Consistency

| Check | Severity | Rule |
|-------|----------|------|
| IDENTITY.md matches SOUL.md | WARN | If both exist, the agent name and vibe in IDENTITY.md should be consistent with any name/personality references in SOUL.md. |

### Skill References

| Check | Severity | Rule |
|-------|----------|------|
| Referenced skills exist | FAIL | All skills mentioned in AGENTS.md or TOOLS.md must have corresponding skill directories with SKILL.md files in skills/. |
| No orphan skill directories | WARN | Skill directories should be referenced somewhere in workspace files. |

### Config Agent ID Consistency

| Check | Severity | Rule |
|-------|----------|------|
| Binding agentIds match agents.list | FAIL | If openclaw.json exists, every `bindings[].agentId` must match one of the `agents.list[].id` values. |
| agents.list exists | WARN | If openclaw.json exists, it should have an `agents.list` array. |

### Binding Completeness

| Check | Severity | Rule |
|-------|----------|------|
| Binding has agentId | WARN | Each binding in `bindings[]` should have an `agentId` field. |
| Binding has match.channel | WARN | Each binding in `bindings[]` should have a `match.channel` field. |
| Binding has target | WARN | Each binding should have a target: `match.peer` or `match.guildId`. |

---

## Hardening Checks

### Boundaries

| Check | Severity | Rule |
|-------|----------|------|
| SOUL.md ## Boundaries section | FAIL | SOUL.md must have a "## Boundaries" section. |
| Privacy boundaries | FAIL | SOUL.md Boundaries section must address privacy (e.g., "Private things stay private"). |
| External action rules | FAIL | SOUL.md or AGENTS.md must have rules about external actions (ask before sending emails, etc.). |
| Scope limits | WARN | SOUL.md or AGENTS.md should define the agent's domain scope. |

### Safety Directives

| Check | Severity | Rule |
|-------|----------|------|
| AGENTS.md ## Safety section | FAIL | AGENTS.md must have a "## Safety" section. |
| No-exfiltration rule | FAIL | AGENTS.md must contain a directive against exfiltrating private data. |
| Destructive command warning | WARN | AGENTS.md should contain guidance about destructive commands (prefer trash over rm, ask before destructive operations). |

### Model Failover

| Check | Severity | Rule |
|-------|----------|------|
| model.fallbacks configured | WARN | If openclaw.json exists and agent is customer-facing, `agents.list[].model.fallbacks` should be defined. |

### Heartbeat Configuration

| Check | Severity | Rule |
|-------|----------|------|
| heartbeat configured | WARN | If openclaw.json exists, at least one agent in `agents.list[]` should have `heartbeat` configured with `heartbeat.every`. Optional: `heartbeat.activeHours`, `heartbeat.model`. |

### Sandbox Configuration

| Check | Severity | Rule |
|-------|----------|------|
| sandbox configured | WARN | If openclaw.json exists, `agents.list[].sandbox` should be configured for non-main sessions. Check for `sandbox.mode` and `sandbox.workspaceAccess`. |

### Tool Execution Security

| Check | Severity | Rule |
|-------|----------|------|
| exec.security set | WARN | If openclaw.json exists and tools are configured, `agents.list[].tools.exec.security` should be set. |
| Tool profile or policies | WARN | If openclaw.json exists, `agents.list[].tools.profile` should be set, or explicit `tools.allow`/`tools.deny` rules should exist. |

### Memory Directives

| Check | Severity | Rule |
|-------|----------|------|
| Daily log directive | FAIL | AGENTS.md must contain directives about daily logs (memory/YYYY-MM-DD.md). |
| Long-term memory directive | FAIL | AGENTS.md must contain directives about MEMORY.md for long-term storage. |
| Write-it-down rule | WARN | AGENTS.md should contain the "write it down / no mental notes" directive or equivalent. |

### Memory Search Configuration

| Check | Severity | Rule |
|-------|----------|------|
| Memory search configured | WARN | If openclaw.json exists, memory search/backend should be configured (or explicitly disabled with justification). |

### Self-Correction

| Check | Severity | Rule |
|-------|----------|------|
| Error journaling | WARN | AGENTS.md should contain directives about logging errors and corrections to memory. |
| Learning loop | WARN | AGENTS.md should contain directives about reviewing past mistakes. |

### Group Chat Behavior

| Check | Severity | Rule |
|-------|----------|------|
| Group chat rules | WARN | If agent is bound to group channels (bindings with guildId), AGENTS.md should define when to speak vs stay silent. |

---

## Config Schema Reference (openclaw.json)

For validation of openclaw.json structure, the following schema fields are relevant:

```
agents.list[].id                    (required string)
agents.list[].model.primary         (optional)
agents.list[].model.fallbacks       (optional array)
agents.list[].tools.profile         (optional)
agents.list[].tools.allow           (optional array)
agents.list[].tools.deny            (optional array)
agents.list[].tools.exec            (optional object)
agents.list[].tools.exec.security   (optional)
agents.list[].heartbeat.every       (optional)
agents.list[].heartbeat.activeHours (optional)
agents.list[].heartbeat.model       (optional)
agents.list[].sandbox.mode          (optional)
agents.list[].sandbox.workspaceAccess (optional)
agents.list[].subagents.maxConcurrent (optional)
agents.list[].subagents.model       (optional)
agents.list[].subagents.thinking    (optional)
agents.list[].groupChat.mentionPatterns (optional)

bindings[].agentId                  (required string)
bindings[].match.channel            (required string)
bindings[].match.peer               (optional string)
bindings[].match.guildId            (optional string)
```
