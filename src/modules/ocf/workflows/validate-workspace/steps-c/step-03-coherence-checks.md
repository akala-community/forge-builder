---
name: 'step-03-coherence-checks'
description: 'Validate cross-artifact consistency: personality alignment, startup references, skill mappings, binding completeness, identity consistency'

nextStepFile: './step-04-hardening-checks.md'
validationRulesRef: '../data/workspace-validation-rules.md'
---

# Step 3: Coherence Checks

## STEP GOAL:

To verify cross-artifact consistency across workspace files -- that references between files are valid, personality definitions are aligned, skill bindings match actual files, and configuration entries are coherent.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step, ensure entire file is read
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are a precision configuration validator (Cog / Gear Wright)
- Systematic, thorough, objective -- reports facts, not opinions
- You bring expertise in cross-artifact validation and workspace consistency

### Step-Specific Rules:

- Focus ONLY on coherence validation (cross-artifact consistency)
- FORBIDDEN to run hardening checks -- that comes in step 04
- FORBIDDEN to re-run structural checks -- that was step 02
- FORBIDDEN to modify any workspace files -- this is a read-only workflow
- If a required file is missing (detected in step 02), skip checks that depend on it and record as "SKIPPED - required file not found"
- If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- Load validation rules for coherence checks
- Read relevant workspace files (SOUL.md, AGENTS.md, IDENTITY.md, openclaw.json)
- Run all coherence checks (C-01 through C-05) against the workspace
- Record each result with severity and detail
- Append findings to the validation report
- Auto-proceed to step 04

## CONTEXT BOUNDARIES:

- Workspace path from step 01
- Workspace file inventory from step 01
- Structural check results from step 02 (to know which files exist)
- Validation report (with structural results) from step 02
- Dependencies: step 01 must be complete; step 02 results available if it ran

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Coherence Validation Rules

Load {validationRulesRef} and read the **Category 2: Coherence Checks** section. Use rules C-01 through C-05 as the check criteria for this step.

### 2. Read Workspace Files for Cross-Reference

Read the following workspace files (if they exist). If a file does not exist, note it as unavailable and skip checks that depend on it.

- `SOUL.md` -- extract agent name, personality traits, communication style, boundaries
- `AGENTS.md` -- extract startup sequence, skill references, session management directives
- `IDENTITY.md` -- extract agent name, emoji, theme
- `openclaw.json` -- parse JSON and extract agents, bindings, channels

### 3. Check SOUL.md and AGENTS.md Personality Consistency (Rule C-01)

**If both SOUL.md and AGENTS.md exist:**

- Extract the agent name from SOUL.md
- Check if AGENTS.md references SOUL.md in its startup/initialization sequence
- Check if the agent name used in AGENTS.md matches or references the name defined in SOUL.md
- PASS if consistent references found
- WARNING if AGENTS.md does not reference SOUL.md or uses a different name

**If either file is missing:**
- Record as SKIPPED with detail noting which file is missing

### 4. Check AGENTS.md Session Startup References (Rule C-02)

**If AGENTS.md exists:**

- Search AGENTS.md for references to the following files:
  - `SOUL.md` (personality loading)
  - `USER.md` (user context loading)
  - `MEMORY.md` or memory-related directives (memory initialization)
- PASS if all three are referenced
- WARNING for each missing reference, with detail: "AGENTS.md does not reference {filename} in startup sequence"

**If AGENTS.md is missing:**
- Record as SKIPPED

### 5. Check Skill References vs Actual Skills (Rule C-03)

**If AGENTS.md exists and skills/ directory exists:**

- Extract skill references from AGENTS.md:
  - Look for skill binding sections, skill lists, or file references matching `skills/*.md` or skill names
- List all `.md` files in the `skills/` directory
- Compare the two lists:
  - Skills referenced in AGENTS.md but missing from skills/ directory: WARNING per missing skill ("Skill '{name}' referenced in AGENTS.md but file not found in skills/")
  - Skill files present in skills/ but not referenced in AGENTS.md: WARNING per orphan ("Skill file '{name}' exists in skills/ but is not referenced in AGENTS.md")
  - Skills that match: PASS per match

**If AGENTS.md is missing or skills/ does not exist:**
- Record as SKIPPED with appropriate detail

### 6. Check openclaw.json Binding Completeness (Rule C-04)

**If openclaw.json exists and was valid JSON (from step 02):**

- Check `agents.list`: Verify each agent entry has a `workspace` path and an `enabled` field
- Check `bindings`: Verify each binding references an agent name that exists in `agents.list`
- Check `bindings`: Verify each binding references a channel that exists in the `channels` section
- PASS if all references are consistent
- WARNING for each broken reference with detail

**If openclaw.json does not exist:**
- Record as SKIPPED with detail "openclaw.json not found -- skipping binding checks"

### 7. Check IDENTITY.md Consistency with SOUL.md (Rule C-05)

**If both IDENTITY.md and SOUL.md exist:**

- Extract the agent name from IDENTITY.md
- Extract the agent name from SOUL.md
- Compare the two:
  - PASS if names match or are clearly the same agent
  - WARNING if names appear to describe different agents, with detail noting the discrepancy

**If either file is missing:**
- Record as SKIPPED with detail noting which file is missing

### 8. Compile Coherence Results

"**Coherence Checks Complete**

---

| Rule | Check | Result | Detail |
|------|-------|--------|--------|
{for each check performed: | rule_id | check_description | PASS/WARNING/ERROR/SKIPPED | detail |}

**Coherence Totals:** {pass_count} PASS / {warning_count} WARNING / {error_count} ERROR / {skipped_count} SKIPPED

---"

Append these results to the Coherence Checks section of the validation report.

### 9. Auto-Proceed

"**Proceeding to hardening checks...**"

**Auto-proceed:** Load, read entire file, then execute {nextStepFile}.

**EXCEPTION:** If the user selected check categories in step 01 that exclude hardening:
- If "coherence only" was selected: Skip to `./step-05-report.md`
- If "all" was selected: Proceed to {nextStepFile} as normal

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- All coherence validation rules (C-01 through C-05) executed or appropriately skipped
- Workspace files read and cross-referenced
- Personality consistency checked between SOUL.md and AGENTS.md
- Startup references validated in AGENTS.md
- Skill references compared against actual skill files
- Binding completeness verified in openclaw.json
- Identity consistency verified between IDENTITY.md and SOUL.md
- All results recorded with severity and detail
- Results appended to validation report
- Auto-proceeding to next step

### FAILURE:

- Not reading the workspace files needed for cross-reference
- Not checking all coherence rules
- Running structural or hardening checks in this step
- Not handling missing files gracefully (should SKIP, not crash)
- Modifying any workspace files

**Master Rule:** Read files, cross-reference content, check consistency. Record every finding. DO NOT run structural or hardening checks, and DO NOT modify any files.
