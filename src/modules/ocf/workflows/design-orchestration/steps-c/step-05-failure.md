---
name: 'step-05-failure'
description: 'Design failure handling patterns including handoff failures, loop prevention, and recovery strategies'

nextStepFile: './step-06-policies.md'
outputFile: '{ocf_output_folder}/orchestration-design-{project_name}.md'
failureReference: '../data/failure-handling-reference.md'
orchestrationReference: '../data/openclaw-orchestration-reference.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
---

# Step 5: Failure Handling

**Progress: Step 5 of 7** — Next: Subagent Policies

## STEP GOAL:

Design failure handling patterns for the orchestration system -- how to handle sub-agent failures, handoff failures, communication timeouts, loop prevention, and recovery strategies. Note that retry/failover is engine-level and not user-configurable. Focus on the parameters that ARE configurable: runTimeoutSeconds, cleanup, maxPingPongTurns, and model.primary/fallbacks.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- ✅ You are a systems architect designing resilience patterns
- ✅ If you already have been given a name, communication_style and persona, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring expertise in distributed system failure patterns — reference {failureReference} and {orchestrationReference} for failure scenarios and config syntax

### Step-Specific Rules:

- 🎯 Focus only on failure handling -- not tool restrictions (Step 6)
- 🚫 FORBIDDEN to design subagent tool policies in this step
- 💬 Approach: Walk through each failure scenario systematically
- 📋 Reference communication patterns from Step 3 to identify failure points
- 🚫 NOTE: Retry/failover is engine-level, NOT user-configurable. Do not generate fabricated retry config blocks.

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append the Failure Handling section to {outputFile} when complete
- 📖 Update frontmatter stepsCompleted to add this step when completed
- 🚫 FORBIDDEN to load next step until user selects 'C'

## CONTEXT BOUNDARIES:

- Available context: Agent Map (Step 2), Communication Patterns (Step 3), Channel Bindings (Step 4)
- Focus: Failure scenarios, recovery strategies, loop prevention
- Limits: Don't configure tool restrictions — that's Step 6
- Dependencies: Communication patterns from Step 3 (spawn/send relationships)

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Identify Failure Points

Using {failureReference}, present the common failure scenarios relevant to the user's communication patterns from Step 3. Ask which are most relevant to their system.

### 2. Design Sub-Agent Failure Handling

For each spawn relationship, collaboratively determine: `runTimeoutSeconds`, timeout action (notify/fallback), error handling strategy, and `cleanup` setting. Reference {failureReference} for config options. Ask 1-2 questions per spawn relationship.

Note: These are the real sessions_spawn parameters: task, label, agentId, model, thinking, runTimeoutSeconds, cleanup. Retry is handled by the engine automatically.

### 3. Design Send Failure Handling

For each send relationship, collaboratively determine: timeout behavior, and `maxPingPongTurns`. Reference {failureReference} for config options.

### 4. Design Loop Prevention

Using {failureReference}, discuss loop prevention strategies relevant to the system. Determine: ping-pong limits, send policy rules, and any channel/chatType restrictions.

### 5. Design Recovery Strategies

Discuss gateway restart recovery, idempotent task design, and monitoring needs. Reference {failureReference} for recovery patterns.

Additionally, configure model fallbacks for resilience:

```json
// Model failover (openclaw.json format)
"model": {
  "primary": "{primary-model-id}",
  "fallbacks": ["{fallback-1}", "{fallback-2}"]
}
```

### 6. Assemble Failure Handling Section

Compile into the output document section with: sub-agent failure policies table, send failure policies table, loop prevention rules, recovery strategies, and send policy configuration.

Present for review — every communication pattern should have a defined failure response.

### 7. Present MENU OPTIONS

Display: "**Select an Option:** [A] Advanced Elicitation [C] Continue"

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF C: Append Failure Handling section to {outputFile}, update frontmatter (add 'step-05-failure' to stepsCompleted), then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#7-present-menu-options)

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN [C continue option] is selected and [Failure Handling section appended to output file with frontmatter updated], will you then load and read fully `{nextStepFile}` to begin subagent policy design.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Every spawn relationship has timeout and error handling defined
- Every send relationship has timeout and recovery defined
- Loop prevention rules are documented
- Recovery strategies are practical and specific
- Send policy configuration is provided
- User has reviewed edge cases

### ❌ SYSTEM FAILURE:

- Communication patterns without failure handling
- No loop prevention strategy
- Generic "handle errors" without specific actions
- Starting tool restriction design (that's Step 6)

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
