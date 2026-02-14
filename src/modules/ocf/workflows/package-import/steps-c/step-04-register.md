---
name: 'step-04-register'
description: 'Register agent entries, set up bindings, and verify the system'

nextStepFile: './step-05-report.md'
installationChecklist: '../data/installation-checklist.md'
reportOutput: '{reportOutput}'
---

# Step 4: Register and Activate

## STEP GOAL:

To register agent entries from the merged configuration, set up channel bindings, verify that all workspace references resolve, and confirm the agent system is ready to activate.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 DO NOT BE LAZY - VERIFY EVERY REGISTRATION
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- ✅ Registration auto-proceeds unless critical failure — no user menus
- ⚙️ If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are the **Registration Specialist** — verifying completeness
- ✅ Check EVERY agent entry and binding

### Step-Specific Rules:

- 🎯 Focus ONLY on registration and activation verification
- 🚫 FORBIDDEN to modify configuration — that was step 03
- 🚫 FORBIDDEN to re-extract files — that was step 02
- 💬 Report findings as [PASS], [FAIL], or [WARN] per check

## EXECUTION PROTOCOLS:

- 🎯 Verify agent entries and bindings in merged configuration
- 💾 Append registration results to {reportOutput}
- 📖 Save report before loading next step
- 🚫 DO NOT halt for user input — auto-proceed

## CONTEXT BOUNDARIES:

- Configuration merge from step 03 is complete
- openclaw.json has been updated with new agent entries and bindings
- Focus on verifying everything is correctly registered
- Dependencies: step 03 must be complete (configuration merged)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Registration Checks

Load {installationChecklist} and focus on the "## Registration Checks" and "## Activation Checks" sections.

### 2. Read Merged Configuration

Read the merged openclaw.json to extract:
- All agent entries added by this import
- All bindings added by this import
- Model configurations for new agents

### 3. Verify Agent Entries

For each new agent entry:

**Agent entry complete:**
- Check: has workspace path
- Check: has agent name
- Check: has model configuration
- Record: [PASS] or [FAIL] with details

**Workspace path resolves:**
- Check: workspace directory exists at the specified path
- Check: SOUL.md exists in workspace
- Check: AGENTS.md exists in workspace
- Record: [PASS] or [FAIL] with details

### 4. Verify Bindings

For each new binding:

**Binding targets valid:**
- Check: has channel defined
- Check: has target (accountId or peer)
- Check: references a registered agent
- Record: [PASS] or [WARN] with details

### 5. Verify Activation Readiness

For each new agent:

**SOUL.md readable:**
- Check: SOUL.md at workspace path is readable and non-empty
- Record: [PASS] or [FAIL]

**AGENTS.md readable:**
- Check: AGENTS.md at workspace path is readable and non-empty
- Record: [PASS] or [FAIL]

**Configuration consistent:**
- Check: agent entry in openclaw.json points to valid workspace
- Check: model configuration references valid provider
- Record: [PASS] or [WARN]

### 6. Append Findings to Report

Replace the "## Registration" and "## Activation Status" sections in {reportOutput} with actual findings:

```markdown
## Registration

### Agent Entries
| Agent | Workspace Path | Model | Status |
|-------|---------------|-------|--------|
| {agent_name} | {workspace_path} | {model} | [PASS/FAIL] |

### Bindings
| Agent | Channel | Target | Status |
|-------|---------|--------|--------|
| {agent_name} | {channel} | {target} | [PASS/WARN] |

### Registration Checks
| Check | Status | Details |
|-------|--------|---------|
| Agent entries complete | [PASS/FAIL] | {details} |
| Workspace paths resolve | [PASS/FAIL] | {details} |
| Binding targets valid | [PASS/WARN] | {details} |

**Registration Summary:** {pass_count} passed, {fail_count} failed, {warn_count} warnings

---

## Activation Status

### Readiness Checks
| Agent | SOUL.md | AGENTS.md | Config | Status |
|-------|---------|-----------|--------|--------|
| {agent_name} | [PASS/FAIL] | [PASS/FAIL] | [PASS/WARN] | {overall} |

**Activation Summary:** {pass_count} passed, {fail_count} failed, {warn_count} warnings
```

### 7. Save Report and Auto-Proceed

"**Registration and activation checks complete.** {pass_count} passed, {fail_count} failed, {warn_count} warnings. Proceeding to final report..."

Save the report, then immediately load, read entire file, then execute {nextStepFile}.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Every agent entry verified
- Every binding verified
- Workspace paths confirmed to resolve
- SOUL.md and AGENTS.md readability confirmed
- Findings appended to report
- Report saved before proceeding
- Auto-proceeded to final report

### ❌ SYSTEM FAILURE:

- Skipping agent entry verification
- Not checking workspace paths resolve
- Not verifying bindings
- Not saving report before proceeding
- Halting for user input

**Master Rule:** Registration checks require VERIFYING every entry. DO NOT BE LAZY. Check EVERY agent and binding. Auto-proceed.
