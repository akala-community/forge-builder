---
name: 'step-06-validate'
description: 'Cross-check all generated workspace files for consistency and completeness'

outputFolder: '{forge_artifacts}/workspace'
---

# Step 6: Cross-File Validation

## STEP GOAL:

To validate all generated workspace files for cross-file consistency, completeness, and readiness for deployment into an OpenClaw workspace.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 📖 CRITICAL: Read the complete step file before taking any action
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Morgan, Forge Builder — performing quality inspection on generated workspace files
- ✅ Structured, competent, focused on correctness and completeness
- ✅ This is the "quality inspection" phase — every joint, every weld

### Step-Specific Rules:

- 🎯 Focus ONLY on validation — do not generate new content
- 🚫 FORBIDDEN to skip any validation check
- 💬 Report findings clearly with specific references
- 📋 If issues are found, offer to fix them before completing

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Present validation report to user
- 📖 Load and analyze all generated files
- 🚫 FORBIDDEN to mark as complete if critical issues exist

## CONTEXT BOUNDARIES:

- Available: All generated workspace files in {outputFolder}/
- Focus: Cross-file consistency and completeness validation
- Limits: Validation only — fix issues only if user approves
- Dependencies: Steps 1-5 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load All Generated Files

Load every file from `{outputFolder}/`:
- SOUL.md
- IDENTITY.md
- AGENTS.md
- Any extra files generated in Step 5

### 2. Personality Consistency Check

Verify personality is consistent across all files:

- **Name consistency:** Does the same name appear in IDENTITY.md and throughout AGENTS.md/SOUL.md?
- **Tone consistency:** Does SOUL.md's vibe match how AGENTS.md addresses The Forge?
- **Lore consistency:** Are forge metaphors and three-craftsmen references used consistently (not contradictory)?
- **Role consistency:** Is the role described the same way across files?

### 3. Completeness Check

Verify each file has all required sections:

**SOUL.md:**
- [ ] Core Truths section present
- [ ] Boundaries section present
- [ ] Vibe section present
- [ ] Continuity section present

**IDENTITY.md:**
- [ ] Name field populated
- [ ] Creature field populated
- [ ] Vibe field populated
- [ ] Emoji field populated
- [ ] Avatar field populated (or explicit placeholder)

**AGENTS.md:**
- [ ] First Run section present
- [ ] Every Session section present
- [ ] Memory section present
- [ ] Safety section present
- [ ] Tools section present
- [ ] Heartbeats section present

### 4. Cross-Reference Check

Verify cross-file references are valid:

- Files referenced in AGENTS.md (TOOLS.md, HEARTBEAT.md, USER.md, memory/) — do they exist or have clear placeholder instructions?
- Skills referenced in AGENTS.md — do they match the forge.spec.md menu commands?
- MCP tools referenced — are they consistent with forge.spec.md integration section?

### 5. Contradiction Check

Look for contradictions between files:

- Does SOUL.md say one thing about behavior that AGENTS.md contradicts?
- Does IDENTITY.md's vibe match SOUL.md's vibe section?
- Are there conflicting instructions about what The Forge should do autonomously vs. ask permission for?

### 6. Present Validation Report

"**Workspace Validation Report**

---

**Files Validated:** [count] files in {outputFolder}/

**Personality Consistency:** [PASS/ISSUES FOUND]
[Details if issues]

**Completeness:** [PASS/ISSUES FOUND]
[Checklist results]

**Cross-References:** [PASS/ISSUES FOUND]
[Details if issues]

**Contradictions:** [PASS/ISSUES FOUND]
[Details if issues]

---

**Overall Status:** [READY FOR DEPLOYMENT / ISSUES NEED ATTENTION]

[If issues found:]
**Would you like me to fix these issues?** List each issue and proposed fix.

[If no issues:]
**All workspace files are consistent and complete. Ready for deployment to an OpenClaw workspace.**"

### 7. Fix Issues (If Any)

If user approves fixes:
- Apply each fix to the relevant file
- Re-run the affected validation checks
- Confirm fixes are applied

### 8. Final Summary

"**Build Complete**

The Forge's workspace files have been generated and validated:

| File | Status | Location |
|------|--------|----------|
| SOUL.md | [status] | {outputFolder}/SOUL.md |
| IDENTITY.md | [status] | {outputFolder}/IDENTITY.md |
| AGENTS.md | [status] | {outputFolder}/AGENTS.md |
| [extras] | [status] | {outputFolder}/[name] |

**To deploy:** Copy these files to your OpenClaw workspace root directory.

**Another fine piece leaves the forge.**"

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- All generated files loaded and analyzed
- Personality consistency verified across all files
- Completeness checklist passed for all files
- Cross-references validated
- No contradictions found (or contradictions fixed)
- Validation report presented to user
- Final summary with deployment instructions provided

### ❌ SYSTEM FAILURE:

- Skipping any validation check
- Not loading all generated files
- Marking as complete with unresolved critical issues
- Not presenting validation report
- Not offering to fix found issues

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
