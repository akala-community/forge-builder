---
conversionFrom: 'src/modules/ocf/workflows/create-skill/create-skill.spec.md'
originalFormat: 'BMAD Module Spec (placeholder)'
workflowName: create-skill
creationDate: 2026-02-11
completionDate: 2026-02-11
status: COMPLETE
confirmationType: conversion
coverageStatus: complete
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-next-step', 'step-10-confirmation', 'step-11-completion']
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/ocf/workflows/create-skill/create-skill.spec.md
**Original Format:** BMAD Module Spec (placeholder)
**Detected Structure:** A placeholder spec defining the intent and rough step outline for a create-skill workflow within the OCF module. No implementation exists.

---

## Original Workflow Analysis

### Goal (from source)

Generate a complete OpenClaw skill with SKILL.md, executable scaffold, and gating rules.

### Original Steps (Complete List)

**Step 1:** Skill Requirements - Gather skill purpose, triggers, inputs/outputs
**Step 2:** Gating Rules - Define OS, binary, and env var requirements
**Step 3:** Code Scaffold - Generate executable scaffold with security compliance
**Step 4:** SKILL.md Generation - Assemble complete SKILL.md with frontmatter

### Output / Deliverable

- `skills/{skill-name}/SKILL.md` -- Complete skill definition
- `skills/{skill-name}/` -- Executable scaffold files (scripts/, references/, assets/)

### Input Requirements

**Required:**
- Skill name and purpose
- Target agent(s) that will use this skill

**Optional:**
- Specific gating requirements
- Code examples or references

### Key Instructions to LLM

- Collaborative, step-by-step creation guided by Cog (Gear Wright) persona
- Security-first: no eval, no exec unless explicitly documented
- Ensure scanner compliance per OpenClaw's `src/security/skill-scanner.ts`
- Follow OpenClaw's SKILL.md patterns (frontmatter with name, description, metadata.openclaw)

---

## Conversion Notes

**What works well in original:**
- Clear 4-step structure mapping to the real skill creation flow
- Good identification of the output artifacts
- Correct agent assignment (Cog/Gear Wright)

**What needs improvement:**
- No implementation exists -- this is purely a spec
- Steps are too coarsely defined for a collaborative workflow
- Missing detail on OpenClaw-specific patterns (frontmatter, scanner rules, gating schema)
- No mention of progressive disclosure patterns or skill naming conventions

**Compliance gaps identified:**
- No step files exist
- No workflow.md exists
- No BMAD-compliant architecture (step-file, frontmatter, menus)
- No continuation/state tracking
- Missing data files for gating rules schema and security patterns

---

## Classification Decisions

**Workflow Name:** create-skill
**Target Path:** _bmad-output/bmb-creations/workflows/create-skill

**4 Key Decisions:**
1. **Document Output:** true (produces SKILL.md and scaffold files)
2. **Module Affiliation:** OCF (OpenClaw Forge)
3. **Session Type:** single-session (focused skill creation)
4. **Lifecycle Support:** create-only (steps-c/ only)

**Structure Implications:**
- Only needs steps-c/ directory
- No step-01b-continue.md needed
- Output is the skill directory itself, not a plan document
- Files are created directly in the target workspace

---

## Requirements

**Flow Structure:**
- Pattern: linear
- Phases: Discovery, Gating, Scaffold, Assembly
- Estimated steps: 4

**User Interaction:**
- Style: guided session (AI leads through structured skill creation)
- Decision points: skill naming, gating rule selection, scaffold type, resource directories
- Checkpoint frequency: after each step

**Inputs Required:**
- Required: Skill name and purpose, target agent(s)
- Optional: Gating requirements, code examples, existing CLI tools to wrap
- Prerequisites: Understanding of what the skill should do

**Output Specifications:**
- Type: document + directory scaffold
- Format: structured (SKILL.md follows strict frontmatter pattern)
- Sections: frontmatter (name, description, metadata.openclaw), body (instructions, examples, references)
- Frequency: single

**Success Criteria:**
- Valid SKILL.md with proper frontmatter (name, description)
- metadata.openclaw block with correct requires/install schemas
- Scaffold directories created as needed (scripts/, references/, assets/)
- Security scanner compliance (no eval, no exec without documentation)
- Skill naming conventions followed (lowercase, hyphens, under 64 chars)

**Instruction Style:**
- Overall: mixed (prescriptive for frontmatter/security, intent-based for content)
- Notes: Cog persona -- precise, technical, configuration-focused

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** excluded - not needed for structured skill creation
- **Advanced Elicitation:** excluded - skill creation is well-defined
- **Brainstorming:** excluded

**LLM Features:**
- **Web-Browsing:** excluded
- **File I/O:** included - creates SKILL.md and scaffold files
- **Sub-Agents:** excluded
- **Sub-Processes:** excluded

**Memory:**
- Type: single-session
- Tracking: none (no continuation needed)

**External Integrations:**
- None

**Installation Requirements:**
- None

---

## Workflow Design

### Step Sequence

**Step 1: Skill Discovery** (Middle/Standard)
- Goal: Gather skill purpose, naming, triggers, target agents, and usage examples
- Actions:
  1. Ask for skill purpose and what it wraps (CLI tool, API, workflow, etc.)
  2. Determine skill name (validate naming conventions)
  3. Identify target agent(s) and trigger phrases
  4. Collect usage examples (how a user would invoke this skill)
  5. Determine which resource directories are needed (scripts/, references/, assets/)
- Output: Skill requirements captured, name validated
- Menu: C only

**Step 2: Gating & Configuration** (Middle/Standard)
- Goal: Define OS, binary, env var requirements and installation instructions
- Actions:
  1. Load gating rules reference data
  2. Determine binary dependencies (bins/anyBins)
  3. Determine environment variable requirements (env)
  4. Determine OS constraints if any (os)
  5. Define installation instructions (brew/node/go/uv/download)
  6. Validate the requires + install schema
- Output: Complete gating rules and install block
- Menu: C only
- Data: gating-rules-schema.md

**Step 3: Code Scaffold & Security** (Middle/Standard)
- Goal: Generate the skill directory structure and any executable scaffold files
- Actions:
  1. Create skill directory at target path
  2. Create resource directories as determined in Step 1
  3. Generate scaffold scripts if needed (with security compliance)
  4. Load security scanner rules reference
  5. Validate all generated code against scanner patterns
  6. Document any intentional exec/spawn usage
- Output: Skill directory with scaffold files
- Menu: C only
- Data: security-scanner-rules.md

**Step 4: SKILL.md Assembly** (Final)
- Goal: Assemble the complete SKILL.md with frontmatter and body
- Actions:
  1. Generate YAML frontmatter (name, description, metadata.openclaw)
  2. Write body with usage instructions, examples, configuration
  3. Apply progressive disclosure patterns if skill is complex
  4. Final review of complete SKILL.md
  5. Present completion summary
- Output: Complete SKILL.md file
- Menu: Final (no next step)
- Template: skill-template.md

### File Structure

```
create-skill/
  workflow.md
  steps-c/
    step-01-discovery.md
    step-02-gating.md
    step-03-scaffold.md
    step-04-assembly.md
  data/
    gating-rules-schema.md
    security-scanner-rules.md
  templates/
    skill-template.md
```

### Role & Persona

- **Role:** Cog (Gear Wright) -- Skills, Config & Assembly Engineer
- **Communication:** Precise and technical. Speaks in terms of configuration and structure.
- **Expertise:** OpenClaw's configuration system, skill architecture, security scanning
- **Tone:** Engineering-focused, collaborative but structured

---

## Foundation Build Complete

**Created:**
- Folder structure at: _bmad-output/bmb-creations/workflows/create-skill
- workflow.md
- Main template: skill-template.md

**Configuration:**
- Workflow name: create-skill
- Continuable: no
- Document output: yes (SKILL.md)
- Mode: create-only

---

## Step 01 Build Complete

**Created:**
- steps-c/step-01-discovery.md

**Step Configuration:**
- Type: Middle/Standard (init step, non-continuable)
- Next Step: step-02-gating

---

## Step 02 Build Complete

**Created:**
- steps-c/step-02-gating.md

**Step Configuration:**
- Type: Middle/Standard
- References: data/gating-rules-schema.md
- Next Step: step-03-scaffold

---

## Step 03 Build Complete

**Created:**
- steps-c/step-03-scaffold.md

**Step Configuration:**
- Type: Middle/Standard
- References: data/security-scanner-rules.md
- Next Step: step-04-assembly

---

## Step 04 Build Complete

**Created:**
- steps-c/step-04-assembly.md

**Step Configuration:**
- Type: Final
- References: templates/skill-template.md, data/gating-rules-schema.md
- Next Step: none (final step)

---

## Conversion Coverage Report

**Source:** src/modules/ocf/workflows/create-skill/create-skill.spec.md
**Target:** _bmad-output/bmb-creations/workflows/create-skill

**Overall Coverage:** 100%

| Category | Total | Covered | Partial | Missing |
|----------|-------|---------|---------|---------|
| Goal | 1 | 1 | 0 | 0 |
| Steps | 4 | 4 | 0 | 0 |
| Instructions | 4 | 4 | 0 | 0 |
| Output | 2 | 2 | 0 | 0 |

**Improvements Made:**
- Deep integration with actual OpenClaw security scanner rules (from src/security/skill-scanner.ts)
- Accurate gating rules schema based on real TypeScript types (from src/agents/skills/types.ts)
- Skill naming validation based on actual conventions from skill-creator SKILL.md
- Progressive disclosure guidance from existing skill patterns
- Cog (Gear Wright) persona integration per agent spec
- Data-driven: gating-rules-schema.md and security-scanner-rules.md reference files
- BMAD-compliant step-file architecture with menus, frontmatter, and sequential enforcement

---

## Completion Summary

**Workflow:** create-skill
**Location:** _bmad-output/bmb-creations/workflows/create-skill/
**Created:** 2026-02-11

**Files Created:**
- workflow.md (entry point)
- 4 step files in steps-c/
- 2 data files in data/
- 1 template in templates/
- 1 workflow plan

**Total: 9 files**
