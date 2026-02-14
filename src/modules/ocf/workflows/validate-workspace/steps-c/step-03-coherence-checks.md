---
name: 'step-03-coherence-checks'
description: 'Validate cross-artifact consistency across workspace files'

nextStepFile: './step-04-hardening-checks.md'
validationRules: '../data/workspace-validation-rules.md'
validationReportOutput: '{validationReportOutput}'
---

# Step 3: Coherence Checks

## STEP GOAL:

Validate cross-artifact consistency -- AGENTS.md references, persona/identity coherence, skill references, openclaw.json agent ID cross-referencing, and binding completeness.

## MANDATORY EXECUTION RULES (READ FIRST):

- DO NOT BE LAZY - READ AND CROSS-REFERENCE EVERY ARTIFACT
- Read the complete step file before taking any action
- When loading next step, ensure entire file is read
- Validation does NOT stop for user input - auto-proceed through all checks
- If any instruction references a tool you lack access to, achieve the outcome in your main context
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`
- Focus ONLY on cross-artifact consistency -- hardening is step 04, structural was step 02
- Report findings as [PASS], [FAIL], or [WARN] per check
- You MUST actually read file contents to perform these checks
- If a required file was missing in step 02, mark checks involving it as [SKIP]

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Validation Rules

Load {validationRules} and focus on the "## Coherence Checks" section.

### 2. Read Workspace Files

Read (if they exist): SOUL.md, AGENTS.md, IDENTITY.md, TOOLS.md, openclaw.json. List all directories under skills/.

### 3. Check AGENTS.md References

AGENTS.md must reference these workspace files at session startup:

- **SOUL.md:** look for "Read SOUL.md" or equivalent, verify file exists -- [PASS] or [FAIL]
- **USER.md:** look for "Read USER.md" or equivalent, verify file exists -- [PASS] or [FAIL]
- **memory/:** look for "memory/YYYY-MM-DD.md", "daily notes", or equivalent, verify directory exists -- [PASS] or [FAIL]
- **MEMORY.md:** look for MEMORY.md reference for main sessions -- [PASS] or [WARN]

### 4. Check Personality-Directive Consistency

- **SOUL.md Boundaries section:** has "## Boundaries" and is non-empty -- [PASS] or [FAIL]
- **Tone consistency:** compare SOUL.md personality with AGENTS.md directives, look for contradictions -- [PASS] or [WARN]

### 5. Check Identity Consistency

If both IDENTITY.md and SOUL.md exist:
- Compare agent name (Name field) and vibe (Vibe field) from IDENTITY.md with SOUL.md references
- [PASS] or [WARN] if names/vibes don't match

If only SOUL.md exists: [PASS] -- no consistency issue.

### 6. Check Skill References

- Extract skill references from AGENTS.md and TOOLS.md
- For each referenced skill, verify directory exists under skills/ with SKILL.md -- [PASS] or [FAIL]
- Check for orphan skill directories not referenced in any workspace file -- [PASS] or [WARN]

### 7. Check Config Agent ID Consistency

If openclaw.json exists with `agents.list`:
- For each `bindings[].agentId`, verify it matches one of `agents.list[].id` -- [PASS] or [FAIL]

If openclaw.json exists but no `agents.list`: [WARN]. If no openclaw.json: [PASS].

### 8. Check Binding Completeness

If openclaw.json has `bindings[]`, for each binding verify:
- Has `agentId` -- [PASS] or [WARN]
- Has `match.channel` -- [PASS] or [WARN]
- Has target (`match.peer` or `match.guildId`) -- [PASS] or [WARN]

If no openclaw.json or no bindings: [PASS].

### 9. Append Findings to Report

Replace "## Coherence Checks" in {validationReportOutput} with tables per category: AGENTS.md References, Personality-Directive Consistency, Identity Consistency, Skill References, Config Agent ID Consistency, Binding Completeness. Each table has columns: `| Check | Status | Details |`. End with: `**Coherence Summary:** {pass_count} passed, {fail_count} failed, {warn_count} warnings`

### 10. Save Report and Auto-Proceed

"**Coherence checks complete.** {pass_count} passed, {fail_count} failed, {warn_count} warnings. Proceeding to hardening checks..."

Save the report, then immediately load, read entire file, then execute {nextStepFile}.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- SOUL.md and AGENTS.md read and cross-referenced
- AGENTS.md references to SOUL.md, USER.md, memory/ verified
- Skill references checked, identity consistency verified
- openclaw.json agent IDs cross-referenced with bindings
- Findings appended to report, report saved, auto-proceeded

### SYSTEM FAILURE:
- Not reading file contents (just checking existence)
- Skipping any coherence check or not cross-referencing between files
- Not verifying openclaw.json agent ID consistency
- Not saving report before proceeding or halting for user input

**Master Rule:** Cross-reference everything. DO NOT BE LAZY. Auto-proceed.
