---
name: 'step-02-structural-checks'
description: 'Verify all required files exist and are well-formed'

nextStepFile: './step-03-coherence-checks.md'
validationRules: '../data/workspace-validation-rules.md'
validationReportOutput: '{validationReportOutput}'
---

# Step 2: Structural Checks

## STEP GOAL:

Verify all required workspace files exist and are well-formed, including skill SKILL.md frontmatter validation.

## MANDATORY EXECUTION RULES (READ FIRST):

- DO NOT BE LAZY - CHECK EVERY FILE AND DIRECTORY
- Read the complete step file before taking any action
- When loading next step, ensure entire file is read
- Validation does NOT stop for user input - auto-proceed through all checks
- If any instruction references a tool you lack access to, achieve the outcome in your main context
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`
- Focus ONLY on structural checks -- cross-artifact consistency is step 03, hardening is step 04
- Report findings as [PASS], [FAIL], or [WARN] per check

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Validation Rules

Load {validationRules} and focus on the "## Structural Checks" section.

### 2. Check Required Files (FAIL if missing)

- **SOUL.md:** exists and is non-empty -- [PASS] or [FAIL]
- **AGENTS.md:** exists and is non-empty -- [PASS] or [FAIL]
- **USER.md:** exists -- [PASS] or [FAIL]
- **IDENTITY.md:** exists -- [PASS] or [WARN] (if absent, check SOUL.md for identity section)

### 3. Check Expected Files (WARN if missing)

- **TOOLS.md:** exists -- [PASS] or [WARN] "Not found -- consider adding if agent uses tools"
- **HEARTBEAT.md:** exists -- [PASS] or [WARN] "Not found -- consider adding if heartbeat is configured"

### 4. Check Optional Files (WARN if missing)

- **MEMORY.md:** exists -- [PASS] or [WARN]
- **BOOT.md:** exists -- [PASS] or [WARN]

### 5. Check Anti-Pattern Files (should NOT exist)

- **BOOTSTRAP.md:** does NOT exist -- [PASS] or [WARN] "Should be deleted after first run"

### 6. Check Directories

- **memory/:** directory exists -- [PASS] or [WARN]
- **skills/:** directory exists -- [PASS] or [WARN]

### 7. Check Skill Well-Formedness

If skills/ exists, for each subdirectory:
- SKILL.md exists inside the directory -- [PASS] or [FAIL]
- SKILL.md has YAML frontmatter with `name` and `description` fields -- [PASS] or [WARN]

If skills/ does not exist: [PASS] -- no skills to validate.

### 8. Check File Well-Formedness

For each existing file, check basic structure:
- **SOUL.md:** has ## sections (Core Truths, Boundaries, Vibe, Continuity) -- [PASS] or [WARN]
- **AGENTS.md:** has ## sections (Every Session, Memory, Safety) -- [PASS] or [WARN]
- **USER.md:** has content (Name, Pronouns, Timezone, Notes, or ## Context) -- [PASS] or [WARN]
- **IDENTITY.md (if exists):** has content (Name, Creature, Vibe, Emoji, Avatar) -- [PASS] or [WARN]
- **HEARTBEAT.md (if exists):** has a periodic task checklist -- [PASS] or [WARN]

### 9. Append Findings to Report

Replace "## Structural Checks" in {validationReportOutput} with tables per category: Required Files, Expected Files, Optional Files, Prohibited Files, Directories, Skill Well-Formedness, File Well-Formedness. Each table has columns: `| Check | Status | Details |`. End with: `**Structural Summary:** {pass_count} passed, {fail_count} failed, {warn_count} warnings`

### 10. Save Report and Auto-Proceed

"**Structural checks complete.** {pass_count} passed, {fail_count} failed, {warn_count} warnings. Proceeding to coherence checks..."

Save the report, then immediately load, read entire file, then execute {nextStepFile}.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:
- Every required, expected, and optional file checked
- Every directory checked
- Skill SKILL.md frontmatter validated
- Well-formedness assessed for all existing files
- Findings appended to report, report saved, auto-proceeded

### SYSTEM FAILURE:
- Skipping any file/directory check
- Not checking skill SKILL.md frontmatter
- Not saving report before proceeding
- Halting for user input

**Master Rule:** Check EVERY file and directory. DO NOT BE LAZY. Auto-proceed.
