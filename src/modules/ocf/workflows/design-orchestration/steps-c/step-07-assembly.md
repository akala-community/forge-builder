---
name: 'step-07-assembly'
description: 'Assemble the complete orchestration design document and generate the openclaw.json configuration fragment'

outputFile: '{ocf_output_folder}/orchestration-design-{project_name}.md'
orchestrationReference: '../data/openclaw-orchestration-reference.md'
---

# Step 7: Assembly & Review

**Progress: Step 7 of 7** — Final Step

## STEP GOAL:

Assemble the complete orchestration design document by generating the openclaw.json configuration fragment that combines all design decisions, then conduct a final review of the entire document.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a systems architect conducting final assembly and review
- ✅ If you already have been given a name, communication_style and persona, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring expertise in OpenClaw configuration and system coherence

### Step-Specific Rules:

- 🎯 Focus on assembling the configuration fragment and final review
- 🚫 FORBIDDEN to redesign previous sections — only fix errors
- 💬 Approach: Generate config from design decisions, then review for coherence
- 📋 Reference {orchestrationReference} for configuration syntax. The configuration fragment should be copy-pasteable into openclaw.json

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append the Configuration Fragment section to {outputFile}
- 📖 Update frontmatter: add 'step-07-assembly' to stepsCompleted, set status to COMPLETE

## CONTEXT BOUNDARIES:

- Available context: Complete document with sections 1-5
- Focus: Configuration generation and coherence review
- Limits: Don't redesign — only fix errors found during review
- Dependencies: All previous steps (2-6)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load Complete Document

Load {outputFile} and review all sections (1-5). Confirm to user that you've loaded the complete design.

### 2. Generate Configuration Fragment

Compile all design decisions into a single openclaw.json5 fragment covering: agents (roster, defaults, subagent config with maxConcurrent/archiveAfterMinutes/model/thinking, tools with profile/allow/alsoAllow/deny/exec, sandbox with mode/workspaceAccess/docker/scope, group chat), bindings (ordered by specificity), model (primary/fallbacks), session policies (ping-pong limits, send policy), and channels.

**CRITICAL:** Use actual values from design decisions in Steps 2-6 — no placeholders.

### 3. Cross-Reference Coherence Check

Verify internal consistency:

1. **Agent references:** Every `agentId` in bindings exists in `agents.list`
2. **Spawn permissions:** Every cross-agent spawn has matching `allowAgents`
3. **Agent-to-agent:** Every `sessions_send` relationship has agents in `agentToAgent.allow`
4. **Binding completeness:** Every channel has a binding
5. **Tool consistency:** No tool conflicts with sandbox mode
6. **Loop safety:** Ping-pong limits and send policies prevent infinite loops
7. **Default agent:** Exactly one agent has `default: true`

Report results and fix any issues found.

### 4. Assemble Configuration Fragment Section

Append to {outputFile}: the complete json5 configuration fragment, coherence check results table, and deployment notes (environment-specific values, channel setup, workspace creation, testing recommendations).

### 5. Final Document Review

Present a summary of the complete document: section counts, coherence status, and ask for final adjustments.

### 6. Finalize Document

Update {outputFile} frontmatter: set stepsCompleted to include all 7 steps, set status to COMPLETE, add completionDate.

### 7. Present Completion Summary

Present the completion summary with: project name, document path, completion date, what was designed (agent/pattern/binding/channel counts), and next steps guidance (review config, create workspaces, set up channels, deploy, test with `openclaw agents list --bindings`).

## CRITICAL STEP COMPLETION NOTE

This is the final step. Present completion summary with the configuration fragment and next steps guidance. No further steps to load.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Configuration fragment generated from actual design decisions (no placeholders)
- Coherence check performed with all checks passing
- Complete document reviewed with user
- Document finalized with COMPLETE status
- Clear next steps provided
- Deployment notes included

### ❌ SYSTEM FAILURE:

- Configuration fragment with placeholder values
- Skipping coherence check
- Not reviewing the complete document
- Missing deployment notes
- Not finalizing document status

**Master Rule:** The configuration fragment must be generated from the actual design decisions made in Steps 2-6. Every value must trace back to a specific user decision.
