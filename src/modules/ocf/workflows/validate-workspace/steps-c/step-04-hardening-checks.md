---
name: 'step-04-hardening-checks'
description: 'Validate security, resilience, and operational hardening: memory directives, tool policies, boundaries, failover, compaction, safety'

nextStepFile: './step-05-report.md'
validationRulesRef: '../data/workspace-validation-rules.md'
---

# Step 4: Hardening Checks

## STEP GOAL:

To verify the workspace is configured for production-grade operation -- checking memory directives, memory backend configuration, tool policies, operational boundaries, model failover chains, compaction settings, and safety guardrails.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step, ensure entire file is read
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are a precision configuration validator (Cog / Gear Wright)
- Systematic, thorough, objective -- reports facts, not opinions
- You bring expertise in production hardening, security posture, and operational resilience

### Step-Specific Rules:

- Focus ONLY on hardening validation (security, resilience, operational readiness)
- FORBIDDEN to re-run structural or coherence checks -- those were steps 02 and 03
- FORBIDDEN to modify any workspace files -- this is a read-only workflow
- If a required file is missing (detected in step 02), skip checks that depend on it and record as "SKIPPED - required file not found"
- Hardening checks use a mix of ERROR, WARNING, and INFO severities -- follow the rules document precisely
- If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context

## EXECUTION PROTOCOLS:

- Load validation rules for hardening checks
- Read relevant workspace files (AGENTS.md, SOUL.md, openclaw.json)
- Run all hardening checks (H-01 through H-07) against the workspace
- Record each result with severity and detail
- Append findings to the validation report
- Auto-proceed to step 05

## CONTEXT BOUNDARIES:

- Workspace path from step 01
- Workspace file inventory from step 01
- Structural check results from step 02 (to know which files exist and if openclaw.json is valid)
- Validation report (with structural and coherence results) from previous steps
- Dependencies: step 01 must be complete; steps 02 and 03 results available if they ran

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Hardening Validation Rules

Load {validationRulesRef} and read the **Category 3: Hardening Checks** section. Use rules H-01 through H-07 as the check criteria for this step.

### 2. Read Workspace Files for Hardening Analysis

Read the following workspace files (if they exist). If a file does not exist, note it as unavailable and skip checks that depend on it.

- `AGENTS.md` -- for memory directives and safety sections
- `SOUL.md` -- for boundaries
- `openclaw.json` -- for memorySearch, tools, model, compaction configuration

### 3. Check Memory Directives in AGENTS.md (Rule H-01)

**If AGENTS.md exists:**

- Search AGENTS.md for memory-related sections or directives
- Look for keywords: memory, remember, recall, persist, save, store, forget, retention
- PASS if memory directives are found with detail noting what was found (e.g., "Memory section found with directives for when to persist and recall")
- WARNING if no memory directives found with detail: "AGENTS.md does not contain explicit memory directives. Production agents should have clear instructions about memory usage."

**If AGENTS.md is missing:**
- Record as SKIPPED

### 4. Check Memory Backend Configuration (Rule H-02)

**If openclaw.json does not exist:**
- Record as INFO with detail: "No openclaw.json found -- memory backend configuration not applicable"

**If openclaw.json exists:**

- Check for `memorySearch` configuration block
- Verify `memorySearch.enabled` is true
- Verify `memorySearch.provider` is set (has a value)
- Verify `memorySearch.store` is set (has a value)
- PASS if all three are configured correctly
- WARNING for each missing or disabled field with specific detail:
  - "memorySearch.enabled is false or missing -- memory search is disabled"
  - "memorySearch.provider is not set -- no memory provider configured"
  - "memorySearch.store is not set -- no memory store configured"

### 5. Check Tool Policies (Rule H-03)

**If openclaw.json does not exist:**
- Record as INFO with detail: "No openclaw.json found -- tool policy configuration not applicable"

**If openclaw.json exists:**

- Check for `tools` configuration block
- Check `tools.profile` value:
  - If set to one of "minimal", "coding", "messaging", "full": PASS with detail noting the profile
  - If missing: WARNING with detail "tools.profile not set -- recommend setting an explicit tool profile"
- Report any `tools.allow` entries (additional tools allowed)
- Report any `tools.deny` entries (tools explicitly denied)
- Check `tools.exec` setting (external command execution)
- Check `tools.web` setting (web access)
- Compile a summary of the tool security posture

### 6. Check Boundaries in SOUL.md (Rule H-04)

**If SOUL.md exists:**

- Search SOUL.md for boundary-related sections or directives
- Look for keywords: boundary, boundaries, limit, forbidden, never, must not, off-limits, scope, refuse, decline, restriction
- PASS if boundaries section or directives are found with detail noting what was found
- WARNING if no boundaries found with detail: "SOUL.md does not contain explicit boundaries. Production agents should have clearly defined operational boundaries."

**If SOUL.md is missing:**
- Record as SKIPPED

### 7. Check Failover Configuration (Rule H-05)

**If openclaw.json does not exist:**
- Record as INFO with detail: "No openclaw.json found -- failover configuration not applicable"

**If openclaw.json exists:**

- Check for `model` configuration block
- Check `model.primary`:
  - If set: note the primary model
  - If missing: WARNING with detail "model.primary is not set"
- Check `model.fallbacks`:
  - If set and contains at least one entry: PASS with detail listing the fallback chain
  - If missing or empty: WARNING with detail "No fallback models configured. If the primary model is unavailable, the agent will fail completely."

### 8. Check Compaction Configuration (Rule H-06)

**If openclaw.json does not exist:**
- Record as INFO with detail: "No openclaw.json found -- compaction configuration not applicable"

**If openclaw.json exists:**

- Check for `compaction` configuration block
- Report `compaction.mode` value:
  - "default" mode: INFO with detail "Compaction mode is 'default'. Consider 'safeguard' mode for better memory preservation in production."
  - "safeguard" mode: PASS with detail "Compaction mode is 'safeguard' -- good for production memory preservation"
  - Not set: INFO with detail "compaction.mode not configured -- defaults will be used"
- Report `compaction.maxHistoryShare` value if set
- Report `compaction.memoryFlush` value if set

### 9. Check Safety Section in AGENTS.md (Rule H-07)

**If AGENTS.md exists:**

- Search AGENTS.md for safety-related sections or directives
- Look for keywords: safety, guardrail, guard, protect, caution, danger, harm, risk, ethics, responsible, harmful, inappropriate
- PASS if safety section or directives are found with detail noting what was found (e.g., "Safety guardrails section found with explicit harm prevention directives")
- WARNING if no safety directives found with detail: "AGENTS.md does not contain explicit safety directives. Production agents should have safety guardrails defined."

**If AGENTS.md is missing:**
- Record as SKIPPED

### 10. Compile Hardening Results

"**Hardening Checks Complete**

---

| Rule | Check | Result | Detail |
|------|-------|--------|--------|
{for each check performed: | rule_id | check_description | PASS/WARNING/ERROR/INFO/SKIPPED | detail |}

**Hardening Totals:** {pass_count} PASS / {warning_count} WARNING / {error_count} ERROR / {info_count} INFO / {skipped_count} SKIPPED

---"

Append these results to the Hardening Checks section of the validation report.

### 11. Auto-Proceed

"**Proceeding to report generation...**"

**Auto-proceed:** Load, read entire file, then execute {nextStepFile}.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- All hardening validation rules (H-01 through H-07) executed or appropriately skipped
- Memory directives checked in AGENTS.md
- Memory backend configuration checked in openclaw.json
- Tool policies analyzed
- Boundaries verified in SOUL.md
- Failover configuration checked
- Compaction settings reviewed
- Safety section verified in AGENTS.md
- All results recorded with correct severity levels (ERROR, WARNING, INFO)
- Results appended to validation report
- Auto-proceeding to report step

### FAILURE:

- Not checking all hardening rules
- Using wrong severity levels (e.g., ERROR where INFO is specified)
- Running structural or coherence checks in this step
- Not handling missing files gracefully (should SKIP, not crash)
- Modifying any workspace files

**Master Rule:** Analyze production readiness systematically. Check memory, tools, boundaries, failover, compaction, and safety. Record every finding with correct severity. DO NOT run structural or coherence checks, and DO NOT modify any files.
