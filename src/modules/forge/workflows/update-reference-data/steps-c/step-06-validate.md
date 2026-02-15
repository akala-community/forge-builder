---
name: 'step-06-validate'
description: 'Cross-validate all updated reference data against OpenClaw source for accuracy'

extractionReportFile: '{output_folder}/extraction-report-{project_name}.md'
patternOutputDir: '../data/patterns'
configRefOutputDir: '../data/config-reference'
---

# Step 6: Validate References

## STEP GOAL:

To cross-check all updated pattern library and config reference data against the OpenClaw source, ensuring every referenced feature exists, no stale references remain, and all data is accurate.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 📋 YOU ARE A FACILITATOR, not a content generator
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a quality assurance analyst for reference data
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring expertise in cross-validation, user reviews results
- ✅ Be adversarial — actively look for errors, not just confirm correctness

### Step-Specific Rules:

- 🎯 Focus only on validation — do NOT modify reference files
- 🚫 FORBIDDEN to update pattern or config reference files in this step
- 💬 Use subprocess Pattern 1 (grep/regex) for cross-validation when available
- 💬 Subprocess returns validation results, not full file contents
- ⚙️ If subprocess unavailable, perform validation in main thread
- 🎯 Report all findings — both passes and failures

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append validation results to {extractionReportFile}
- 📖 Update extraction report frontmatter stepsCompleted
- 🚫 This is the final step — mark workflow complete when done

## CONTEXT BOUNDARIES:

- Available: Complete extraction report, all pattern and config ref files
- Focus: Cross-validation of references against source
- Limits: Read-only — do not modify reference files
- Dependencies: All previous steps must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load All Reference Data

Load the extraction report from {extractionReportFile} to get the source root path.

Load all pattern files from {patternOutputDir}.
Load all config reference files from {configRefOutputDir}.

"**Beginning cross-validation of all reference data.**

**Loaded:**
- Pattern files: {count}
- Config reference files: {count}
- Source root: {path from extraction report}"

### 2. Validate Pattern References

Launch a subprocess (or work in main thread) that:
1. For each pattern file, extract all referenced OpenClaw features
2. Search the OpenClaw source to verify each referenced feature exists
3. Return validation results:

```yaml
results:
  - pattern: pattern_name
    status: PASS|FAIL
    referenced_features:
      - name: feature_name
        exists_in_source: true|false
        source_location: path/to/file.ts:line
```

"**Pattern Validation Results:**

| Pattern | Status | Issues |
|---------|--------|--------|
{table of results}"

### 3. Validate Config References

Launch a subprocess (or work in main thread) that:
1. For each config reference entry, verify the config key exists in source
2. Verify type, default, and description match source
3. Return validation results:

```yaml
results:
  - config_key: key_name
    status: PASS|FAIL
    checks:
      exists_in_source: true|false
      type_matches: true|false
      default_matches: true|false
```

"**Config Reference Validation Results:**

| Config Key | Status | Issues |
|------------|--------|--------|
{table of results}"

### 4. Check for Stale References

Launch a subprocess (or work in main thread) that:
1. Grep all pattern and config reference files for feature/config names
2. Cross-reference against the extraction report
3. Identify any references to items not in the extraction report (stale)

"**Stale Reference Check:**
- Stale pattern references: {count}
- Stale config references: {count}
{list any stale references found}"

### 5. Generate Final Validation Report

Compile all validation results into a summary:

"**VALIDATION SUMMARY**

**Overall Status:** {PASS / FAIL}

**Pattern Library:**
- Total patterns: {count}
- Passing: {count}
- Failing: {count}
- Stale references: {count}

**Config Reference:**
- Total entries: {count}
- Passing: {count}
- Failing: {count}
- Stale references: {count}

**Issues Found:**
{list any issues, or 'None — all references validated successfully'}

**Recommendation:** {proceed / fix issues before using}"

### 6. Append Validation to Extraction Report

Append the validation report to {extractionReportFile} under `## Validation Results`.

Update frontmatter:
- Add `'step-06-validate'` to `stepsCompleted`
- Set `status: COMPLETE` if all pass, or `status: NEEDS_REVIEW` if failures

### 7. Final Summary

"**Reference data update complete.**

**Files updated:**
- Pattern library: {patternOutputDir} ({count} files)
- Config reference: {configRefOutputDir} ({count} files)
- Extraction report: {extractionReportFile}

**Validation:** {PASS/FAIL}

The Forge's reference data is now {up to date / needs review before use}."

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All pattern references validated against source
- All config references validated against source
- Stale reference check completed
- Validation report generated and appended
- Final summary presented to user
- Extraction report marked complete

### ❌ SYSTEM FAILURE:

- Skipping validation checks
- Not checking for stale references
- Modifying reference files during validation
- Not generating validation report
- Not marking workflow complete

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
