---
name: 'step-04-hardening-checks'
description: 'Verify security, resilience, and operational hardening'

nextStepFile: './step-05-report.md'
validationRules: '../data/workspace-validation-rules.md'
validationReportOutput: '{validationReportOutput}'
---

# Step 4: Hardening Checks

## STEP GOAL:

Verify security, resilience, and operational hardening -- boundaries, safety rules, model failover, heartbeat, sandbox, tool execution security, memory directives, memory search config, self-correction, and group chat behavior.

## MANDATORY EXECUTION RULES (READ FIRST):

- DO NOT BE LAZY - CHECK EVERY HARDENING RULE
- Read the complete step file before taking any action
- When loading next step, ensure entire file is read
- Validation does NOT stop for user input - auto-proceed through all checks
- If any instruction references a tool you lack access to, achieve the outcome in your main context
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`
- Focus ONLY on hardening checks -- structural was step 02, coherence was step 03
- Report findings as [PASS], [FAIL], or [WARN] per check
- You MUST actually read AGENTS.md, SOUL.md, and openclaw.json content
- If a required file was missing, mark checks involving it as [SKIP]

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Validation Rules

Load {validationRules} and focus on the "## Hardening Checks" section.

### 2. Read Workspace Files

Read (if not already read): AGENTS.md, SOUL.md, openclaw.json (if exists).

### 3. Check Boundaries (SOUL.md)

- **## Boundaries section exists** -- [PASS] or [FAIL]
- **Privacy boundaries:** search for "private", "privacy", "stay private", "confidential" -- [PASS] or [FAIL]
- **External action rules:** search for "ask before", "ask first", "external", "sending" -- [PASS] or [FAIL]
- **Scope limits:** search for domain/scope limitations in SOUL.md or AGENTS.md -- [PASS] or [WARN]

### 4. Check Safety Directives (AGENTS.md)

- **## Safety section exists** -- [PASS] or [FAIL]
- **No-exfiltration rule:** search for "exfiltrate", "private data" -- [PASS] or [FAIL]
- **Destructive command warning:** search for "destructive", "rm", "trash", "delete" -- [PASS] or [WARN]

### 5. Check Model Failover (openclaw.json)

If openclaw.json exists: check `agents.list[].model.fallbacks` -- [PASS] or [WARN].
If no openclaw.json: [WARN] "Cannot verify failover."

### 6. Check Heartbeat Configuration (openclaw.json)

If openclaw.json exists: check `agents.list[].heartbeat` for `every`, optionally `activeHours` and `model` -- [PASS] or [WARN].
If no openclaw.json: [WARN] "Cannot verify heartbeat config."

### 7. Check Sandbox Configuration (openclaw.json)

If openclaw.json exists: check `agents.list[].sandbox` for `mode` and `workspaceAccess` -- [PASS] or [WARN].
Non-main sessions should have sandbox configured for isolation.
If no openclaw.json: [WARN] "Cannot verify sandbox config."

### 8. Check Tool Execution Security (openclaw.json)

If openclaw.json exists:
- Check `agents.list[].tools.exec.security` is set -- [PASS] or [WARN]
- Check `tools.profile` is set or explicit `tools.allow`/`tools.deny` rules exist -- [PASS] or [WARN]

If no openclaw.json: [WARN] "Cannot verify tool execution security."

### 9. Check Memory Directives (AGENTS.md)

- **Daily log directive:** search for "memory/YYYY-MM-DD.md", "daily notes", "daily logs" -- [PASS] or [FAIL]
- **Long-term memory directive:** search for MEMORY.md references -- [PASS] or [FAIL]
- **Write-it-down rule:** search for "write it down", "mental notes", "Text > Brain" -- [PASS] or [WARN]

### 10. Check Memory Search Configuration (openclaw.json)

If openclaw.json exists: check memory section and backend/search config -- [PASS] or [WARN].
If no openclaw.json: [WARN] "Cannot verify memory search config."

### 11. Check Self-Correction Directives (AGENTS.md)

- **Error journaling:** search for "mistake", "error", "correction", "log" -- [PASS] or [WARN]
- **Learning loop:** search for "review", "past mistakes", "recurring", "patterns" -- [PASS] or [WARN]

### 12. Check Group Chat Behavior

If agent bound to group channels (openclaw.json bindings with `guildId`):
- Search AGENTS.md for "group chat", "when to speak", "stay silent", "HEARTBEAT_OK" -- [PASS] or [WARN]

If not bound to group channels: [PASS] -- not applicable.

### 13. Append Findings to Report

Replace "## Hardening Checks" in {validationReportOutput} with tables per category: Boundaries, Safety Directives, Model Failover, Heartbeat Configuration, Sandbox Configuration, Tool Execution Security, Memory Directives, Memory Search Configuration, Self-Correction, Group Chat Behavior. Each table has columns: `| Check | Status | Details |`. End with: `**Hardening Summary:** {pass_count} passed, {fail_count} failed, {warn_count} warnings`

### 14. Save Report and Auto-Proceed

"**Hardening checks complete.** {pass_count} passed, {fail_count} failed, {warn_count} warnings. Proceeding to final report..."

Save the report, then immediately load, read entire file, then execute {nextStepFile}.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- Every hardening rule checked across all categories
- AGENTS.md, SOUL.md, openclaw.json read and analyzed
- Boundaries, safety, failover, heartbeat, sandbox, tool security, memory, self-correction all checked
- Findings appended to report, report saved, auto-proceeded

### SYSTEM FAILURE:
- Skipping any hardening check
- Not reading file contents deeply
- Not checking sandbox, exec.security, or memory search config
- Not saving report before proceeding or halting for user input

**Master Rule:** Check EVERY hardening rule. DO NOT BE LAZY. Auto-proceed.
