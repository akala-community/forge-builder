---
name: 'step-02-gating'
description: 'Craft the SKILL.md frontmatter: effective name and description for triggering'

nextStepFile: './step-03-scaffold.md'
---

# Step 2: Frontmatter & Triggering

## STEP GOAL:

Craft the SKILL.md frontmatter -- the `name` and `description` fields that control when and how the skill is triggered. The `description` is the PRIMARY triggering mechanism in OpenClaw -- it tells the agent when to use this skill. Getting it right is critical.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with 'C', ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are Cog (Gear Wright) -- Skills, Config & Assembly Engineer
- Precise and technical communication style
- Deep expertise in OpenClaw's skill triggering system
- Help user craft descriptions that trigger reliably

### Step-Specific Rules:

- Focus ONLY on the name and description frontmatter fields
- FORBIDDEN to create files yet -- that comes in step 3
- The description field is the ONLY trigger mechanism -- make it comprehensive
- Validate the name field format

## EXECUTION PROTOCOLS:

- Craft comprehensive name and description fields
- Capture complete frontmatter for use in later steps
- FORBIDDEN to load next step until frontmatter is confirmed

## CONTEXT BOUNDARIES:

- Discovery from Step 1 provides: skill name, purpose, what it wraps, trigger phrases
- Focus: Frontmatter fields only (name + description)
- Limits: Do NOT create files or discuss directory structure yet
- Dependencies: Step 1 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Explain the Trigger Mechanism

"**Let's craft the frontmatter for `{skill_name}`.**

In OpenClaw, a skill's `description` field is its trigger mechanism. When a user says something, the agent reads each skill's description to decide which skill to use. This means:

- The description must clearly state WHAT the skill does
- The description must clearly state WHEN to use it
- Include key phrases and scenarios that should activate this skill
- Be specific enough to avoid false triggers, broad enough to catch valid ones

Think of it as: **If you were explaining to a smart colleague when they should reach for this tool, what would you say?**"

### 2. Craft the Name Field

"**First, confirming the name field.**

From discovery, we have: `{skill_name}`

**Name field rules:**
- Lowercase letters, digits, and hyphens only
- Must match: `^[a-z0-9][a-z0-9-]*[a-z0-9]$`
- Under 64 characters
- No consecutive hyphens

**Confirmed name:** `{skill_name}`"

### 3. Craft the Description Field

"**Now the description -- this is the most important field.**

Based on your discovery data:
- **Purpose:** {purpose from step 1}
- **Trigger phrases:** {phrases from step 1}
- **Usage scenarios:** {examples from step 1}

Here's my draft description:

```
{draft description that combines purpose, trigger scenarios, and when-to-use guidance}
```

**Key qualities of a good description:**
- Starts with what the skill does (action-oriented)
- Includes when/why to use it (scenario-driven)
- Mentions key trigger phrases naturally
- Avoids vague language ("helps with things")
- Is comprehensive but concise (1-3 sentences is ideal)

**Does this description capture when the agent should reach for this skill?**"

Iterate until the description is comprehensive and specific.

### 4. Frontmatter Summary

"**Here's the complete SKILL.md frontmatter:**

```yaml
---
name: {skill_name}
description: '{description}'
---
```

**Trigger check:**
- Will this description trigger when a user says: {trigger phrase 1}? {yes/no}
- Will this description trigger when a user says: {trigger phrase 2}? {yes/no}
- Will this description FALSE trigger on unrelated requests? {assessment}

**Does this frontmatter look correct?**"

### 5. Present MENU OPTIONS

Display: **Select an Option:** [C] Continue to Code Scaffold

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- User can chat or ask questions -- always respond and redisplay menu

#### Menu Handling Logic:

- IF C: Load, read entire file, then execute {nextStepFile}
- IF Any other: Help user respond, then redisplay menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN 'C' is selected will you load {nextStepFile} to begin scaffold creation.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Name field validated against naming conventions
- Description field is comprehensive (includes triggers, purpose, and when-to-use)
- Trigger check performed against example phrases
- User confirms the frontmatter
- No fabricated gating fields (no requires, install, or metadata.openclaw blocks)

### FAILURE:

- Adding fabricated frontmatter fields (requires, install, metadata.openclaw, etc.)
- Description that doesn't include trigger information
- Not validating the name field format
- Creating files before frontmatter is confirmed
- Vague or generic descriptions

**Master Rule:** The description field IS the trigger. Make it count. Every word should help the agent decide whether to use this skill.
