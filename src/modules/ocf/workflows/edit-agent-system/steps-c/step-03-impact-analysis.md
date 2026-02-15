---
name: 'step-03-impact-analysis'
description: 'Analyze cross-artifact implications of requested changes'

nextStepFile: './step-04-apply-changes.md'
outputFile: '{ocf_output_folder}/change-reports/change-report-{date}.md'
artifactTypesData: '../data/artifact-types.csv'
coherenceRulesData: '../data/coherence-rules.csv'
impactMatrixData: '../data/impact-matrix.csv'
---

# Step 3: Impact Analysis

## STEP GOAL:

To analyze the cross-artifact implications of every requested change, identifying which files need modification, what specific changes are needed in each, and flagging potential coherence risks.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a systems architect analyzing change propagation
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ Channel Vulcan (Forge Master) for architectural perspective
- ✅ Think in terms of artifact dependencies and ripple effects

### Step-Specific Rules:

- 🎯 Focus only on ANALYSIS -- do not apply any changes
- 🚫 FORBIDDEN to modify any workspace files
- 💬 Present analysis clearly so user can approve before application
- ⚙️ Use subprocess optimization (Pattern 2) for per-artifact analysis if available. TOOL/SUBPROCESS FALLBACK: If subprocess unavailable, perform analysis in main thread

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append impact analysis to {outputFile}
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to proceed until user approves the impact analysis

## CONTEXT BOUNDARIES:

- Change specifications are documented in the change report (from step 2)
- Full workspace inventory is available (from step 1)
- Focus: Understanding the FULL SCOPE of what needs to change
- Limits: Analysis only -- no modifications

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Analysis Context

Load `{outputFile}` to get the change specifications from step 2.
Load `{artifactTypesData}` for artifact relationships.
Load `{impactMatrixData}` for change propagation rules.
Load `{coherenceRulesData}` for consistency requirements.

### 2. Analyze Each Change

**DO NOT BE LAZY -- For EACH change in the specification list:**

Analyze the change against the impact matrix:

**a. Identify primary artifact modifications:**
- What specifically needs to change in the primary artifact?
- Line-level specificity where possible

**b. Identify secondary artifact propagations:**
- Using the impact matrix, determine which secondary artifacts are affected
- For each secondary artifact, determine what specifically needs to change

**c. Check coherence rules:**
- For each affected artifact pair, check applicable coherence rules
- Flag any rules that could be violated by this change

**d. Identify risks:**
- Are there circular dependencies?
- Could this change break existing functionality?
- Are there ambiguities in how to propagate?

### 3. Build Impact Map

Create a comprehensive impact map:

"**Impact Analysis Results:**

### Change {N}: {change description}

**Primary Modification:**
- **File:** {file path}
- **What changes:** {specific modification}

**Propagation to Secondary Artifacts:**

| Artifact | What Changes | Coherence Rule | Risk |
|----------|-------------|----------------|------|
| {artifact} | {specific change} | {rule_id} | {low/medium/high} |
| {artifact} | {specific change} | {rule_id} | {low/medium/high} |

**Total Files Affected:** {count}
**Coherence Rules Involved:** {list rule_ids}
**Risk Level:** {low/medium/high}

---

{Repeat for each change}"

### 4. Present Combined Impact Summary

"**Combined Impact Analysis:**

**Total Changes Requested:** {count}
**Total Files to Modify:** {count unique files}
**Total Coherence Rules Engaged:** {count}
**Overall Risk Level:** {low/medium/high}

**Modification Plan:**

| File | Changes From | Modifications |
|------|-------------|---------------|
| SOUL.md | Change 1, 3 | {list modifications} |
| AGENTS.md | Change 1, 2 | {list modifications} |
| ... | ... | ... |

**Potential Risks:**
{List any high or medium risks with explanations}

**Recommendations:**
{Any suggestions for the user -- e.g., 'Consider also updating X' or 'This change is safe and straightforward'}"

### 5. User Review and Approval

"**Please review the impact analysis above.**

- Are there any modifications you want to exclude?
- Any additional artifacts you think should be updated?
- Any concerns about the identified risks?

**Once you approve, I'll proceed to apply these modifications.**"

Wait for user confirmation. If user wants changes, update the analysis and re-present.

### 6. Append to Change Report

Append to `{outputFile}`:

```markdown
## Impact Analysis Results

**Analysis Date:** {current date}
**Total Files Affected:** {count}
**Overall Risk Level:** {risk}

### Per-Change Analysis

{Full impact analysis from step 3}

### Combined Modification Plan

{Modification plan table from step 4}

### Identified Risks

{Risk list}

### User Approval

{User's approval or modifications to the plan}
```

Update frontmatter:
- Add 'step-03-impact-analysis' to stepsCompleted
- Set lastStep to 'step-03-impact-analysis'

### 7. Present Menu Options

Display: "**Impact analysis complete and approved. Select an Option:** [C] Continue to Apply Changes"

#### Menu Handling Logic:

- IF C: Save analysis to {outputFile}, update frontmatter, then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#7-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- User can chat or ask questions -- always respond and then redisplay menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and the impact analysis is saved with user approval will you then load and read fully `{nextStepFile}` to execute change application.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Every requested change analyzed for cross-artifact impact
- Impact matrix and coherence rules consulted
- Primary and secondary modifications identified per-file
- Risks flagged and communicated
- User reviews and approves the analysis
- Impact analysis saved to change report

### ❌ SYSTEM FAILURE:

- Skipping analysis for any change
- Not checking secondary artifact propagation
- Not consulting coherence rules
- Modifying any workspace files
- Proceeding without user approval

**Master Rule:** Analyze EVERY change against EVERY relevant artifact. Miss nothing. The quality of the analysis determines the quality of the edits.
