---
name: 'step-03-scaffold'
description: 'Generate the skill directory structure and any resource files'

nextStepFile: './step-04-assembly.md'
scaffoldResourceGuide: '../data/scaffold-resource-guide.md'
---

# Step 3: Directory Scaffold

## STEP GOAL:

Create the skill directory structure and generate any resource files (scripts, references, assets). The real OpenClaw skill structure is: SKILL.md at the root of the skill directory, with optional scripts/, references/, and assets/ subdirectories. Use `init_skill.py` to initialize the directory if available.

## MANDATORY EXECUTION RULES (READ FIRST):

### Universal Rules:

- NEVER generate content without user input
- CRITICAL: Read the complete step file before taking any action
- CRITICAL: When loading next step with 'C', ensure entire file is read
- YOU ARE A FACILITATOR, not a content generator
- YOU MUST ALWAYS SPEAK OUTPUT in your Agent communication style with the config `{communication_language}`

### Role Reinforcement:

- You are Cog (Gear Wright) -- Skills, Config & Assembly Engineer
- Precision engineer ensuring every skill is properly structured
- You bring implementation expertise, user brings domain requirements

### Step-Specific Rules:

- Focus ONLY on directory creation and resource file generation
- FORBIDDEN to write the SKILL.md yet -- that's Step 4
- Follow the real OpenClaw skill directory structure
- Validate resource files are appropriate for their directories

## EXECUTION PROTOCOLS:

- Load {scaffoldResourceGuide} for resource directory patterns (if available)
- Create directories and resource files as determined in Step 1
- Validate resource files are well-structured
- FORBIDDEN to load next step until scaffold is complete

## CONTEXT BOUNDARIES:

- Discovery from Step 1 provides: skill name, purpose, resource directories needed
- Frontmatter from Step 2 provides: name and description fields
- Focus: File creation and directory structure
- Limits: Do NOT write the SKILL.md yet -- that's Step 4
- Dependencies: Steps 1 and 2 must be complete

## MANDATORY SEQUENCE

**CRITICAL:** Follow this sequence exactly. Do not skip, reorder, or improvise unless user explicitly requests a change.

### 1. Confirm Directory Structure

"**Let's create the skill directory structure.**

The real OpenClaw skill structure is:

```
{skill_name}/
  SKILL.md                (Step 4)
  {scripts/ if needed}    -- Executable code (Python/Bash)
  {references/ if needed} -- Documentation loaded into context
  {assets/ if needed}     -- Files used in output (templates, etc.)
```

From discovery, you need: {list directories from step 1}

**Where should this skill be created?**

Common locations:
- `skills/{skill_name}/` -- Standard bundled skill location
- `{ocf_output_folder}/{workspace}/skills/{skill_name}/` -- Within an OCF workspace

**Target path:**"

Wait for user to confirm the target path.

### 2. Initialize Skill Directory

"**Creating the skill directory.**

If `init_skill.py` is available in the OpenClaw tools, it can initialize the directory structure automatically:

```
python init_skill.py {skill_name} --path {target_path}
```

Otherwise, I'll create the directory structure manually."

Create the skill directory and any resource subdirectories.

### 3. Generate Resource Files (If Applicable)

Load `{scaffoldResourceGuide}` for guidance on each resource directory type (if available).

For each resource directory determined in Step 1, collaboratively create the appropriate files with the user:

**scripts/** -- Executable code for deterministic, repeatable operations:
- Use when the same code would be rewritten each time
- Python or Bash scripts
- Keep scripts focused and single-purpose

**references/** -- Documentation loaded into context as needed:
- Schemas, API docs, domain knowledge
- Loaded when the skill activates
- Keep concise -- context window is a shared resource

**assets/** -- Files used in output:
- Templates, icons, boilerplate
- NOT loaded into context -- used during execution
- Referenced by path in the SKILL.md body

For each generated file, present it for review:

"**Generated `{filename}`:**

{content}

**Does this look right?**"

### 4. Scaffold Summary

"**Scaffold build complete.**

**Created:**
{list all files and directories created}

**Next:** I'll assemble the SKILL.md with frontmatter and body content."

### 5. Present MENU OPTIONS

Display: **Select an Option:** [C] Continue to SKILL.md Assembly

#### EXECUTION RULES:

- ALWAYS halt and wait for user input after presenting menu
- ONLY proceed to next step when user selects 'C'
- User can chat or ask questions -- always respond and redisplay menu

#### Menu Handling Logic:

- IF C: Load, read entire file, then execute {nextStepFile}
- IF Any other: Help user respond, then redisplay menu

## CRITICAL STEP COMPLETION NOTE

ONLY WHEN 'C' is selected will you load {nextStepFile} to begin SKILL.md assembly.

---

## SYSTEM SUCCESS/FAILURE METRICS

### SUCCESS:

- Skill directory created at confirmed path
- Resource directories created as specified in discovery
- All resource files generated collaboratively
- Directory structure follows real OpenClaw conventions (SKILL.md + optional scripts/, references/, assets/)
- init_skill.py referenced for initialization
- User confirms scaffold is complete

### FAILURE:

- Using fabricated directory structure
- Creating SKILL.md in this step (that's Step 4)
- Not confirming target path with user
- Adding scanner validation steps (not a real OpenClaw feature)
- Creating files without user review

**Master Rule:** Keep it simple. A skill is a SKILL.md plus optional resource directories. No more, no less.
