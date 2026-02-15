---
name: 'step-02-identify-changes'
description: 'Collaboratively determine what the user wants to modify in the workspace'

nextStepFile: './step-03-impact-analysis.md'
outputFile: '{ocf_output_folder}/change-reports/change-report-{date}.md'
artifactTypesData: '../data/artifact-types.csv'
impactMatrixData: '../data/impact-matrix.csv'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
---

# Step 2: Identify Changes

## STEP GOAL:

To collaboratively determine what the user wants to modify in their workspace -- which agent(s), which artifact types, and the specific nature of the changes.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a change analyst helping users articulate their edit requirements
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring OCF architecture expertise to help users express changes precisely

### Step-Specific Rules:

- 🎯 Focus only on IDENTIFYING changes -- do not analyze impact or apply anything
- 🚫 FORBIDDEN to modify any workspace files
- 🚫 FORBIDDEN to perform impact analysis -- that's step 3
- 💬 Approach: Ask clarifying questions, categorize changes, confirm understanding

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append change specifications to {outputFile}
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to proceed until changes are clearly specified

## CONTEXT BOUNDARIES:

- Workspace is loaded and inventoried (from step 1)
- Agent roster and artifact inventory are available in the change report
- Focus: Understanding WHAT the user wants to change
- Limits: Do not analyze impact or make modifications yet

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Review Workspace Context

Load `{outputFile}` to review the workspace summary from step 1.

"**Your workspace has {agent_count} agent(s): {agent_names}**

What would you like to change? You can describe your changes in natural language -- I'll help structure them.

**Common change types:**
- Persona or identity changes (name, personality, communication style)
- Skill changes (add, remove, or modify skills)
- Configuration changes (bindings, channels, tool policies)
- Memory or context changes (memory scaffolds, recall patterns)
- Orchestration changes (agent communication, routing)
- Boundary or safety changes (restrictions, guardrails)"

Wait for user's description of desired changes.

### 2. Clarify and Categorize Changes

Based on the user's description, ask targeted follow-up questions:

**For persona changes:**
- "Which agent's persona should change?"
- "What specific traits or behaviors should be different?"
- "Should the communication style change?"

**For skill changes:**
- "Which agent's skills are affected?"
- "Is this an addition, removal, or modification?"
- "What should the skill do differently?"

**For config changes:**
- "Which configuration areas are affected?"
- "Are there new channels or bindings to add?"
- "Should tool access change?"

**For orchestration changes:**
- "How should agent communication change?"
- "Are there new routing rules?"
- "Should any spawn/send relationships change?"

Ask 1-2 questions at a time. Think about responses before asking more.

### 3. Load Change Type References

Load `{artifactTypesData}` and `{impactMatrixData}` to understand the formal change categories.

Map the user's natural language changes to formal change types from the impact matrix.

### 4. Structure the Change Specification

For each identified change, create a structured specification:

"**I've identified the following changes:**

**Change {N}:**
- **Type:** {change_type from impact matrix}
- **Agent:** {agent_name or "system-wide"}
- **Primary Artifact:** {artifact that will be directly modified}
- **Description:** {what specifically changes}
- **User Intent:** {why the user wants this change}

{Repeat for each change}

**Is this accurate? Would you like to add, remove, or modify any of these change specifications?**"

Iterate until the user confirms the change list.

### 5. Confirm Final Change List

"**Final Change List:**

| # | Type | Agent | Primary Artifact | Description |
|---|------|-------|------------------|-------------|
| 1 | {type} | {agent} | {artifact} | {description} |
| 2 | {type} | {agent} | {artifact} | {description} |
| ... | ... | ... | ... | ... |

**Total Changes:** {count}

**Next step:** I'll analyze the impact of these changes across all workspace artifacts to identify everything that needs to be updated.

**Does this change list look complete?**"

### 6. Append to Change Report

Append to `{outputFile}`:

```markdown
## Changes Requested

**Date:** {current date}
**Requested by:** {user_name}

### Change Specifications

{Full change specification table}

### Change Details

{For each change, the detailed specification from step 4}
```

Update frontmatter:
- Add 'step-02-identify-changes' to stepsCompleted
- Set lastStep to 'step-02-identify-changes'

### 7. Present Menu Options

Display: "**Changes identified and documented. Select an Option:** [A] Advanced Elicitation [C] Continue to Impact Analysis"

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF C: Save changes to {outputFile}, update frontmatter, then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#7-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu
- User can chat or ask questions -- always respond and then redisplay menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and the change specifications are saved to the change report will you then load and read fully `{nextStepFile}` to execute impact analysis.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- User's desired changes clearly understood through conversation
- Changes categorized using formal change types from impact matrix
- Each change has: type, agent, primary artifact, description, intent
- User confirms the change list is complete and accurate
- Change specifications saved to change report

### ❌ SYSTEM FAILURE:

- Assuming changes without user confirmation
- Not categorizing changes formally
- Proceeding with vague or unclear change descriptions
- Modifying any workspace files
- Performing impact analysis (that's step 3)

**Master Rule:** Understand EXACTLY what the user wants to change before analyzing impact. Precision here prevents problems later.
