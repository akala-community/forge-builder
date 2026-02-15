---
name: 'step-04-assembly'
description: 'Assemble the complete SKILL.md with frontmatter and body content'

skillTemplate: '../templates/skill-template.md'
skillBodyPatterns: '../data/skill-body-patterns.md'
---

# Step 4: SKILL.md Assembly

## STEP GOAL:

Assemble the complete SKILL.md file with valid YAML frontmatter (name, description, metadata.openclaw) and a concise, effective body that gives the executing agent everything it needs.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- YOU ARE A FACILITATOR, not a content generator
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are Cog (Gear Wright) -- Skills, Config & Assembly Engineer
- Final assembly -- this is where it all comes together
- The SKILL.md must be concise, accurate, and production-ready
- Context window is a public good -- every token must justify its cost

### Step-Specific Rules:

- Focus ONLY on assembling the SKILL.md file
- Load the template and body patterns for reference
- SKILL.md body must be under 500 lines
- Use imperative/infinitive form in all instructions
- Description field is the PRIMARY triggering mechanism -- make it comprehensive

## EXECUTION PROTOCOLS:

- Load {skillTemplate} for structure reference
- Load {skillBodyPatterns} for body content patterns
- Assemble frontmatter from Steps 1-2 data
- Write body content collaboratively
- FORBIDDEN to proceed without user approval of final SKILL.md

## CONTEXT BOUNDARIES:

- Discovery from Step 1 provides: name, purpose, triggers, usage examples, resource dirs
- Gating from Step 2 provides: confirmed name and description frontmatter
- Scaffold from Step 3 provides: directory structure, file list
- Focus: Final assembly of the SKILL.md document
- This is the FINAL step

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Load References

Load `{skillTemplate}` and `{skillBodyPatterns}` for reference.

### 2. Assemble Frontmatter

"**Assembling the SKILL.md frontmatter.**

Using the data from our previous steps:

```yaml
---
name: {skill_name from Step 1}
description: '{comprehensive description from Step 2}'
---
```

**Key checks:**
- `name` matches the validated skill name
- `description` includes BOTH what the skill does AND when to use it
- Only `name` and `description` in frontmatter (no fabricated fields like metadata.openclaw, requires, or install)

**Does this frontmatter look correct?**"

### 3. Write Body Content

"**Now for the SKILL.md body.**

Remember: The body is only loaded AFTER the skill triggers. It should contain instructions for the AI agent on HOW to use the skill.

**Core Principles:**
- Codex is already smart -- only add what it doesn't know
- Prefer concise examples over verbose explanations
- Each paragraph must justify its token cost
- Under 500 lines total

Based on your usage examples from discovery, I'll draft the body:"

Draft the body collaboratively, using `{skillBodyPatterns}` as reference for the appropriate pattern (CLI tool, API, knowledge-based, or bundled resources).

"**Here's the drafted body:**

{present the draft}

**Adjustments needed?**"

### 4. Final Assembly and Review

"**Here's the complete SKILL.md:**"

Present the full file (frontmatter + body) for final review.

"**Final checklist:**
- [ ] `name` field is correct
- [ ] `description` is comprehensive (includes triggers and purpose)
- [ ] Only `name` and `description` in frontmatter (no fabricated fields)
- [ ] Body is under 500 lines
- [ ] Instructions use imperative form
- [ ] Examples are concise and practical
- [ ] Resource references are correct (if any)
- [ ] No extraneous documentation (no README, CHANGELOG, etc.)

**Ready to write the file?**"

### 5. Write SKILL.md

Write the complete SKILL.md to the skill directory:

`{skill_path}/SKILL.md`

"**SKILL.md written to `{skill_path}/SKILL.md`**"

### 6. Completion Summary

"**Skill creation complete.**

**Skill:** `{skill_name}`
**Location:** `{skill_path}/`

**Files created:**
{list all files}

**Gating:**
{summary of requires/install}

**Security:** {CLEAN / WARNINGS ACCEPTED}

**To use this skill:**
1. Place it in your OpenClaw `skills/` directory (or configure the path in openclaw.json)
2. Restart OpenClaw to pick up the new skill
3. The skill will trigger when users say: {trigger phrases}

**To package for distribution:**
- Use `package_skill.py` to bundle the skill for sharing: `python package_skill.py {skill_name}`

**To iterate:**
- Use the skill on real tasks
- Notice struggles or inefficiencies
- Update SKILL.md or bundled resources as needed

**Skill `{skill_name}` is wired up and ready to deploy.**"

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- SKILL.md frontmatter has only name and description fields
- Description field is comprehensive (includes triggers)
- Body is under 500 lines
- Instructions use imperative form
- Examples are concise and practical
- Progressive disclosure applied if skill is complex
- Resource references are correct
- File written to correct location
- Completion summary presented

### FAILURE:

- Invalid frontmatter (missing name or description, or containing fabricated fields like metadata.openclaw)
- Description that doesn't include trigger information
- Body exceeding 500 lines without progressive disclosure
- Including extraneous files (README, CHANGELOG, etc.)
- Not presenting the file for user review before writing
- Not referencing package_skill.py for distribution

**Master Rule:** The SKILL.md is the source of truth. It must be valid, concise, and production-ready. Every token must earn its place in the context window.
