---
conversionFrom: 'src/modules/ocf/workflows/create-single-agent/create-single-agent.spec.md'
originalFormat: 'BMAD Module Spec (placeholder)'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-next-step', 'step-10-confirmation', 'step-11-completion']
created: 2026-02-11
completionDate: 2026-02-11
status: COMPLETE
workflowName: create-single-agent
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/ocf/workflows/create-single-agent/create-single-agent.spec.md
**Original Format:** BMAD Module Spec (placeholder)
**Detected Structure:** 3-step create-only workflow specification for streamlined single agent workspace creation

---

## Original Workflow Analysis

### Goal (from source)

Streamlined workflow for creating a single agent workspace (brief + generation in one flow). Combines the brief and generation phases into a single streamlined flow for users who need just one agent. Produces a complete single-agent workspace with all artifacts.

### Original Steps (Complete List)

**Step 1:** Quick Brief - Gather agent concept, persona, skills, and channel needs in one pass
**Step 2:** Identity & Config - Generate SOUL.md, AGENTS.md, USER.md, MEMORY.md, skills, and config
**Step 3:** Assembly - Assemble single-agent workspace and present for review

### Output / Deliverable

Complete single-agent workspace at `{ocf_output_folder}/{agent-name}/` containing:
- SOUL.md (persona/identity)
- AGENTS.md (directives)
- USER.md (user context)
- MEMORY.md (memory architecture)
- Skills folder
- Configuration fragments (openclaw.json)

### Input Requirements

**Required:**
- User's single agent concept (gathered through conversation)

**Optional:**
- Channel requirements (WhatsApp, Discord, Slack, etc.)
- Existing OpenClaw workspace to integrate with

### Key Instructions to LLM

The workflow uses Anima (Soul Smith) persona — creative, empathetic, identity-focused. Collaborative facilitation style where Anima guides users through concept definition, then generates all artifacts. The streamlined nature means brief + generation happen in one flow without handoffs to other agents.

---

## Conversion Notes

**What works well in original:**
- Clear 3-step structure that's genuinely streamlined
- Good separation of concerns (gather → generate → assemble)
- Single agent (Anima) handling everything reduces complexity

**What needs improvement:**
- Spec only — no actual implementation exists
- No detailed step instructions, menus, or templates
- Missing output template definition
- Missing workspace structure specification

**Compliance gaps identified:**
- No workflow.md entry point
- No step files
- No output templates
- No frontmatter or state tracking
- No menu patterns or continuation support

---

## Classification Decisions

**Workflow Name:** create-single-agent
**Target Path:** {project-root}/_bmad/ocf/workflows/create-single-agent

**4 Key Decisions:**
1. **Document Output:** true (produces a complete workspace with multiple files)
2. **Module Affiliation:** OCF module (`_bmad/ocf/workflows/create-single-agent`)
3. **Session Type:** single-session (streamlined flow designed for completion in one sitting)
4. **Lifecycle Support:** create-only (steps-c/ only — this is a streamlined creation flow)

**Structure Implications:**
- Needs steps-c/ folder only (no steps-e/ or steps-v/)
- No step-01b-continue.md needed (single-session)
- Output is a workspace directory, not a single document
- Uses OCF module config variables (ocf_output_folder)

---

## Requirements

**Flow Structure:**
- Pattern: linear (brief → generate → assemble → review)
- Phases: 3 major phases
- Estimated steps: 3 create steps

**User Interaction:**
- Style: mixed (highly collaborative in step 01 briefing, mostly autonomous in step 02 generation, collaborative review in step 03)
- Decision points: agent concept, persona choices, skill selection, channel requirements, final review
- Checkpoint frequency: after each step

**Inputs Required:**
- Required: Agent concept (gathered through guided conversation)
- Optional: Channel requirements, existing workspace path
- Prerequisites: OCF module installed with config

**Output Specifications:**
- Type: workspace directory (multiple documents)
- Format: structured workspace with predefined artifact types
- Files: SOUL.md, AGENTS.md, USER.md, MEMORY.md, skills/, config fragments
- Frequency: single workspace per execution

**Success Criteria:**
- Complete workspace generated with all required artifacts
- Artifacts are internally coherent (persona aligns with directives, skills match capabilities)
- User reviews and approves final workspace
- Workspace is ready for deployment or further hardening

**Instruction Style:**
- Overall: mixed
- Step 01: collaborative/facilitative (gathering concept)
- Step 02: mostly autonomous with checkpoints (generating artifacts)
- Step 03: collaborative (review and refinement)

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** excluded (streamlined flow doesn't need creative exploration)
- **Advanced Elicitation:** included in Step 01 (for deeper concept exploration if needed)
- **Brainstorming:** excluded (concept gathering is built into step 01)

**LLM Features:**
- **Web-Browsing:** excluded (not needed for agent creation)
- **File I/O:** included (writes workspace files)
- **Sub-Agents:** excluded (Anima handles everything)
- **Sub-Processes:** excluded (linear flow)

**Memory:**
- Type: single-session
- Tracking: internal state only (no stepsCompleted in output — output is workspace files, not a document)

**External Integrations:**
- None required

**Installation Requirements:**
- OCF module must be installed
- No additional dependencies

---

## Design

### Step Structure

**Step 01 - Quick Brief (Middle/Standard with A/C menu)**
- Goal: Gather complete agent concept in one guided conversation pass
- Type: Collaborative facilitation
- Sections to cover: concept, persona/voice, skills/capabilities, channel needs, boundaries
- Menu: [A] Advanced Elicitation [C] Continue
- Output: Internal state (agent brief data) carried to next step

**Step 02 - Identity & Config Generation (Middle/Simple with C menu)**
- Goal: Generate all workspace artifacts from the brief
- Type: Mostly autonomous with review checkpoints
- Generates: SOUL.md, AGENTS.md, USER.md, MEMORY.md, skills, openclaw.json fragments
- Menu: [C] Continue to Assembly
- Output: Generated artifacts held in memory for assembly

**Step 03 - Assembly & Review (Final step)**
- Goal: Assemble workspace directory, present for review, allow refinements
- Type: Collaborative review
- Actions: Create workspace folder, write all artifacts, present summary, allow edits
- Menu: [R] Refine [F] Finalize - no next step (final)
- Output: Complete workspace at {ocf_output_folder}/{agent-name}/

### Interaction Pattern Design

- Step 01: Guided conversation with structured sections, user provides concept
- Step 02: Anima generates autonomously, presents each artifact for quick review
- Step 03: Full workspace review with option to refine individual artifacts

### Data Flow Design

- Step 01 → Step 02: Agent brief (concept, persona, skills, channels, boundaries)
- Step 02 → Step 03: Generated artifacts (SOUL.md, AGENTS.md, USER.md, MEMORY.md, skills, config)
- Step 03 → Output: Complete workspace directory

### File Structure Design

```
create-single-agent/
├── workflow.md
├── steps-c/
│   ├── step-01-quick-brief.md
│   ├── step-02-identity-config.md
│   └── step-03-assembly.md
└── templates/
    ├── soul-template.md
    ├── agents-template.md
    ├── user-template.md
    └── memory-template.md
```

### Role and Persona Definition

- Role: Anima (Soul Smith) — Persona & Identity Designer
- Expertise: Identity architecture, persona crafting, coherent agent design
- Communication: Creative, empathetic, focused on personality and purpose
- Style: "What kind of voice should this agent have? What makes it unique?"

---

## Foundation Build Complete

**Created:**
- Folder structure at: {project-root}/_bmad/ocf/workflows/create-single-agent
- workflow.md
- Templates: soul-template.md, agents-template.md, user-template.md, memory-template.md

**Configuration:**
- Workflow name: create-single-agent
- Continuable: no
- Document output: yes (workspace directory)
- Mode: create-only

---

## Step 01 Build Complete

**Created:**
- steps-c/step-01-quick-brief.md

**Step Configuration:**
- Type: non-continuable, standard middle step
- Outputs: agent brief data (internal state)
- Next Step: step-02-identity-config

---

## Step 02 Build Complete

**Created:**
- steps-c/step-02-identity-config.md

**Step Configuration:**
- Type: mostly autonomous generation step
- Outputs: generated artifacts (SOUL.md, AGENTS.md, USER.md, MEMORY.md, skills, config)
- Next Step: step-03-assembly

---

## Step 03 Build Complete

**Created:**
- steps-c/step-03-assembly.md

**Step Configuration:**
- Type: final step (assembly + review)
- Outputs: complete workspace directory
- Next Step: none (final step)
