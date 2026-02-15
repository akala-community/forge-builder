---
name: 'step-03-format-complete'
description: 'Assemble final configuration, generate merge instructions, and complete workflow'

outputFile: '{output_folder}/openclaw-config-{project_name}.md'
mergeInstructions: '../data/merge-instructions.md'
---

# Step 3: Format & Complete

## STEP GOAL:

Assemble all extracted configuration fragments into a complete, merge-ready openclaw.json structure, generate clear merge instructions for each section, optionally produce a merge preview, and complete the workflow.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER modify extracted fragments at this stage — only assemble and format
- 📖 CRITICAL: Read the complete step file before taking any action
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are Cog (Gear Wright) — precision configuration engineer
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring assembly and integration expertise
- ✅ User confirms everything is complete and ready for deployment

### Step-Specific Rules:

- 🎯 Focus ONLY on assembly, merge instructions, and completion
- 🚫 FORBIDDEN to re-extract or modify fragment contents
- 💬 Present the complete assembled configuration clearly
- 🚪 This is the final step

## EXECUTION PROTOCOLS:

- 🎯 Assemble complete configuration from extracted fragments
- 💾 Finalize the output document
- 📖 Update frontmatter with completion status
- 🚫 No more extraction at this stage

## CONTEXT BOUNDARIES:

- All configuration domains have been extracted in Step 2
- The output document contains all fragment sections
- This is the final step — assemble, instruct, and complete
- Focus: Assembly, merge instructions, optional merge preview

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise.

### 1. Load Output Document and Merge Reference

Load `{outputFile}` completely. Review all extracted fragment sections from Step 2.

Load `{mergeInstructions}` for assembly rules and per-section merge guidance.

### 2. Assemble Complete Configuration

Combine all extracted fragments into a single, valid openclaw.json structure following the assembly rules in {mergeInstructions}.

### 3. Generate Merge Instructions

Using the section merge guide from {mergeInstructions}, present specific merge guidance for each configuration section and list all `[SET_*]` placeholder markers that need resolution.

### 4. Generate Merge Preview (If Merge Target Provided)

**Check frontmatter `hasMergeTarget`:**

**IF merge target was provided:**

Load the existing openclaw.json from `{mergeTargetPath}`. Perform a simulated deep merge following the merge preview rules in {mergeInstructions}.

Present the merged result with a summary of changes (new agents, bindings, other additions).

**IF no merge target:**

"**No merge target was provided. Use the merge instructions above to manually integrate the fragments into your existing openclaw.json.**"

### 5. Append to Output Document

Append the following to {outputFile}:

- **Merge Instructions** section — complete merge guidance
- **Complete Configuration Fragment** section — assembled JSON
- **Merge Preview** section — merged result (if applicable) or note that no preview was requested

### 6. Finalize Output Document

Update {outputFile} frontmatter:

```yaml
stepsCompleted: ['step-01-load-workspace', 'step-02-extract-fragments', 'step-03-format-complete']
lastStep: 'step-03-format-complete'
status: COMPLETE
completionDate: {current date}
```

### 7. Present Completion Summary

"**Configuration Export Complete**

**System:** {systemName}
**Workspace:** {workspacePath}
**Date:** {current date}
**Agents Exported:** {agentCount}

| Domain | Status |
|--------|--------|
| Agent Entries | ✅ {count} agents exported |
| Bindings | ✅ {count} bindings / ⚠️ {count} placeholder IDs |
| Tool Policies | ✅ {count} agents configured |
| Memory | ✅ Configured |
| Model / Failover | ✅ {count} agents / ⚠️ {count} placeholders |
| Heartbeat | ✅ {count} agents / ⏭️ Skipped |
| Logging | ✅ Configured |

**Placeholders to resolve:** {count}
**Merge preview:** {generated / not requested}"

### 8. Provide Next Steps

"**Next Steps:**

1. **Review** the exported configuration at `{outputFile}`
2. **Resolve** all `[SET_*]` placeholder markers with your actual values
3. **Merge** the fragments into your existing openclaw.json using the merge instructions
4. **Validate** your openclaw.json — run the **validate-workspace** workflow to check consistency
5. **Test** each agent's configuration in a development environment before production

**Your configuration export is saved at:** `{outputFile}`"

### 9. Final Completion Message

"**Cog, signing off. Your configuration fragments are ready for deployment.**

Every agent, binding, policy, and configuration has been extracted and formatted for clean integration into your existing OpenClaw installation.

**Configuration export:** `{outputFile}`"

## CRITICAL STEP COMPLETION NOTE

This is the final step. Present the assembled configuration, merge instructions, and completion summary. No further steps to load.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Complete configuration assembled into valid JSON structure
- Clear merge instructions generated for each section
- All placeholder markers documented
- Merge preview generated (if merge target provided)
- Output document finalized with COMPLETE status
- User has clear next steps for applying the configuration

### ❌ SYSTEM FAILURE:

- Invalid JSON structure in assembled configuration
- Missing merge instructions for any domain
- Undocumented placeholder markers
- Not finalizing output document status
- No guidance on applying the configuration

**Master Rule:** End with a clear, complete export. The user should know exactly what was extracted and exactly how to merge it into their existing openclaw.json.
