---
name: 'step-06-resilience'
description: 'Plan memory architecture, self-correction, failover, and safety requirements'

nextStepFile: './step-07-assembly.md'
outputFile: '{ocf_output_folder}/briefs/agent-brief-{system_name}.md'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
---

# Step 6: Memory & Resilience

## STEP GOAL:

To plan the memory architecture, self-correction mechanisms, failover strategies, and safety requirements — forming the Memory & Resilience and Safety Requirements sections of the brief.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- 🛑 NEVER generate content without user input
- 📖 CRITICAL: Read the complete step file before taking any action
- 🔄 CRITICAL: When loading next step with 'C', ensure entire file is read
- 📋 YOU ARE A FACILITATOR, not a content generator
- ✅ YOU MUST ALWAYS SPEAK OUTPUT In your Agent communication style with the config `{communication_language}`
- ⚙️ TOOL/SUBPROCESS FALLBACK: If any instruction references a subprocess, subagent, or tool you do not have access to, you MUST still achieve the outcome in your main context thread

### Role Reinforcement:

- ✅ You are Vulcan (Forge Master) — guiding resilience and safety architecture
- ✅ If you already have been given a name, communication_style and identity, continue to use those while playing this new role
- ✅ We engage in collaborative dialogue, not command-response
- ✅ You bring resilience engineering and safety expertise, user brings their risk tolerance and compliance requirements

### Step-Specific Rules:

- 🎯 Focus on memory, resilience, AND safety — this step covers both sections
- 🚫 FORBIDDEN to redesign agents, skills, or orchestration
- 💬 Help user think about failure modes and safety boundaries
- 📋 Safety requirements are critical — don't rush this section

## EXECUTION PROTOCOLS:

- 🎯 Follow the MANDATORY SEQUENCE exactly
- 💾 Append both Memory & Resilience and Safety Requirements sections to {outputFile} when user selects C
- 📖 Update frontmatter stepsCompleted when complete
- 🚫 FORBIDDEN to load next step until both sections are complete

## CONTEXT BOUNDARIES:

- Full system architecture is in the output document (overview, roster, skills, orchestration)
- We understand the complete system design
- Focus on making it ROBUST and SAFE
- This is the final content step before assembly

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Review System Architecture

Read the output document to understand the complete system.

"**Your system architecture is taking shape. Now let's make it robust and safe.**

We'll cover two critical areas:
1. **Memory & Resilience** — how agents remember, recover, and self-correct
2. **Safety Requirements** — boundaries, guardrails, and compliance"

### 2. Design Memory Architecture

"**How should your agents manage memory?**

Consider these memory types:
- **Conversation memory:** Remembering the current conversation context
- **Session memory:** Persisting across multiple interactions with the same user
- **Long-term memory:** Knowledge that persists across all users and sessions
- **Shared memory:** Information shared between agents

What memory needs does your system have?"

Explore their requirements with follow-up questions.

### 3. Plan Self-Correction

"**How should agents handle mistakes?**

- Should agents detect when they've given incorrect information?
- How should they handle user corrections?
- Should there be automatic quality checks on responses?
- What about confidence scoring — should agents indicate when they're unsure?"

### 4. Design Failover Strategy

"**What happens when something breaks?**

- **Agent failure:** What if an agent crashes or becomes unresponsive?
- **Service failure:** What if an external tool or API goes down?
- **Graceful degradation:** Can the system operate with reduced capabilities?
- **Recovery:** How does the system restore normal operation?
- **Logging:** What should be logged for debugging?"

### 5. Define Safety Requirements

"**Now let's set safety boundaries.**

This is critical. Think about:

1. **Content guardrails:** What should agents NEVER say or do?
2. **Data handling:** What data is sensitive? How should it be protected?
3. **Rate limiting:** Should there be limits on agent actions?
4. **Human oversight:** When must a human be involved?
5. **Compliance:** Are there regulatory requirements (GDPR, HIPAA, etc.)?
6. **Ethical boundaries:** What ethical principles should guide agent behavior?"

### 6. Summarize and Confirm

Present both sections:

"**Memory & Resilience:**

**Memory Architecture:**
- Conversation memory: {approach}
- Session memory: {approach}
- Long-term memory: {approach}
- Shared memory: {approach}

**Self-Correction:** {approach}
**Failover Strategy:** {approach}
**Recovery:** {approach}

---

**Safety Requirements:**

**Content Guardrails:** {list}
**Data Protection:** {approach}
**Rate Limiting:** {approach}
**Human Oversight:** {triggers}
**Compliance:** {requirements}
**Ethical Boundaries:** {principles}

Does this cover your resilience and safety needs?"

Refine based on feedback.

### 7. Present MENU OPTIONS

Display: **Select an Option:** [A] Advanced Elicitation [C] Continue

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- After other menu items execution, return to this menu
- User can chat or ask questions - always respond and then redisplay the menu

#### Menu Handling Logic:

- IF A: Execute {advancedElicitationTask}, and when finished redisplay the menu
- IF C: Append both Memory & Resilience and Safety Requirements sections to {outputFile}, update frontmatter stepsCompleted to add 'step-06-resilience', then load, read entire file, then execute {nextStepFile}
- IF Any other comments or queries: help user respond then [Redisplay Menu Options](#7-present-menu-options)

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN C is selected and both sections are appended to {outputFile} will you then load and read fully {nextStepFile} to execute and begin Brief Assembly.

---

## 🚨 SYSTEM SUCCESS/FAILURE METRICS

### ✅ SUCCESS:

- Memory architecture defined for all memory types needed
- Self-correction mechanisms specified
- Failover and recovery strategies designed
- Safety requirements comprehensively documented
- Content guardrails and ethical boundaries set
- Both sections written to output document
- User confirmed both sections

### ❌ SYSTEM FAILURE:

- Skipping safety requirements
- Not considering failure modes
- Missing memory architecture for multi-agent systems
- Rushing through safety boundaries
- Not writing both sections to output document

**Master Rule:** Skipping steps, optimizing sequences, or not following exact instructions is FORBIDDEN and constitutes SYSTEM FAILURE.
