---
name: 'step-03-configure'
description: 'Merge openclaw.json configuration fragments into existing configuration'

nextStepFile: './step-04-register.md'
installationChecklist: '../data/installation-checklist.md'
reportOutput: '{reportOutput}'
---

# Step 3: Configure

## STEP GOAL:

To merge the package's openclaw.json configuration fragments into the existing OpenClaw configuration, handling conflicts and preserving existing settings.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 DO NOT BE LAZY - CHECK EVERY CONFIGURATION SECTION
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step, ensure entire file is read
- ⚙️ If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are the **Configuration Specialist** — careful, non-destructive merging
- ✅ NEVER overwrite existing configuration without user confirmation
- ✅ Preserve all existing settings that don't conflict

### Step-Specific Rules:

- 🎯 Focus ONLY on configuration merging
- 🚫 FORBIDDEN to register agents — that's step 04
- 🚫 FORBIDDEN to re-extract files — that was step 02
- 💬 Report findings as [PASS], [FAIL], or [WARN] per check
- 📖 You MUST read both existing and package configuration completely

## EXECUTION PROTOCOLS:

- 🎯 Load both configurations and plan the merge
- 💬 Present conflicts to user for resolution
- 💾 Append configuration changes to {reportOutput}
- 📖 Save report before loading next step

## CONTEXT BOUNDARIES:

- Extraction from step 02 confirmed workspace files are in place
- Focus on openclaw.json merging only
- If no openclaw.json fragment exists in package, skip merge and record [PASS]
- Dependencies: step 02 must be complete (files extracted)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Configuration Merge Checks

Load {installationChecklist} and focus on the "## Configuration Merge Checks" section.

### 2. Locate Configuration Files

**Find existing openclaw.json:**
- Search project root for openclaw.json
- If not found: record [WARN] "No existing openclaw.json — package config will be installed fresh"

**Find package configuration fragment:**
- Search extracted workspace for openclaw.json, openclaw.fragment.json, or configuration section in setup.md
- If not found: record [PASS] "No configuration fragment in package — no merge needed" and auto-proceed to next step

### 3. Read Both Configurations

**If both exist:**
- Read existing openclaw.json completely
- Read package configuration fragment completely

Present both:

"**Existing configuration sections:**
- agents: {count} entries
- bindings: {count} entries
- models: {section present/absent}
- tools: {section present/absent}

**Package configuration adds:**
- agents: {count} new entries
- bindings: {count} new entries
- models: {changes if any}
- tools: {changes if any}"

### 4. Identify Merge Points

For each configuration section:

**Agents section:**
- List new agent entries from package
- Check for name conflicts with existing agents
- Record: [PASS] per non-conflicting entry, [WARN] per conflict

**Bindings section:**
- List new bindings from package
- Check for channel conflicts
- Record: [PASS] per non-conflicting binding, [WARN] per conflict

**Models section:**
- Identify model configuration changes
- Record: [PASS] or [WARN]

**Tools section:**
- Identify tool configuration changes
- Record: [PASS] or [WARN]

### 5. Handle Conflicts

**If conflicts detected:**

"**Configuration conflicts detected:**

{For each conflict:}
**Conflict:** {description}
**Existing:** {current value}
**Package:** {new value}

**How would you like to resolve this?**
- **[K]eep existing** — Keep current configuration
- **[U]se package** — Use the package's value
- **[M]erge** — Combine both (if applicable)"

Wait for user resolution on each conflict.

**If no conflicts:**
"**No configuration conflicts detected. Proceeding with merge.**"

### 6. Perform Merge

Apply the merge based on conflict resolutions:

- Add new agent entries
- Add new bindings
- Apply model changes (if approved)
- Apply tool changes (if approved)

Write the merged openclaw.json.

### 7. Append Findings to Report

Replace the "## Configuration Changes" section in {reportOutput} with actual findings:

```markdown
## Configuration Changes

**Existing Config:** {path to openclaw.json}
**Package Fragment:** {path to fragment}

### Merge Summary
| Section | Added | Modified | Conflicts | Resolution |
|---------|-------|----------|-----------|------------|
| agents | {n} | {n} | {n} | {details} |
| bindings | {n} | {n} | {n} | {details} |
| models | {n} | {n} | {n} | {details} |
| tools | {n} | {n} | {n} | {details} |

### Configuration Checks
| Check | Status | Details |
|-------|--------|---------|
| openclaw.json exists | [PASS/WARN] | {details} |
| No agent name conflicts | [PASS/WARN] | {details} |
| Binding channels valid | [PASS/WARN] | {details} |
| Model references valid | [PASS/WARN] | {details} |

**Configuration Summary:** {pass_count} passed, {fail_count} failed, {warn_count} warnings
```

### 8. Present Summary and Proceed

"**Configuration merge complete.** {pass_count} passed, {fail_count} failed, {warn_count} warnings."

Display: **[C] Continue to Registration**

#### Menu Handling Logic:

- IF C: Save report, then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then redisplay menu

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Both configurations read completely
- All merge points identified
- Conflicts detected and presented to user
- User-approved merge performed
- Merged openclaw.json written
- Findings appended to report
- Report saved before proceeding

### ❌ SYSTEM FAILURE:

- Overwriting existing configuration without user confirmation
- Not detecting conflicts
- Skipping configuration sections
- Not saving report before proceeding

**Master Rule:** Configuration merge must be NON-DESTRUCTIVE. NEVER overwrite existing settings without explicit user approval. Check EVERY section.
