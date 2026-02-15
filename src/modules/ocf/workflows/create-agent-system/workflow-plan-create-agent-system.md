---
conversionFrom: 'src/modules/ocf/workflows/create-agent-system/create-agent-system.spec.md'
originalFormat: 'BMAD Workflow Spec (placeholder)'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-steps', 'step-10-confirmation', 'step-11-completion']
created: 2026-02-11
completionDate: 2026-02-11
status: COMPLETE
approvedDate: 2026-02-11
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/ocf/workflows/create-agent-system/create-agent-system.spec.md
**Original Format:** BMAD Workflow Spec (placeholder — not yet implemented)
**Detected Structure:** 8-step create-only workflow specification with agent assignments and output definitions

---

## Original Workflow Analysis

### Goal (from source)

Take a structured brief and generate the complete OpenClaw workspace with all artifacts — including AGENTS.md, SOUL.md, USER.md, MEMORY.md scaffolds, skills directory, REVIEW.md, openclaw.json configuration fragments, and workspace directory structure for every agent in the system.

### Original Steps (Complete List)

**Step 1:** Load Brief - Load and validate the agent system brief
**Step 2:** Identity Generation - Generate SOUL.md and AGENTS.md for each agent (Anima phase)
**Step 3:** Context Generation - Generate USER.md templates and MEMORY.md scaffolds per agent
**Step 4:** Skill Generation - Generate skills directory with SKILL.md files per agent
**Step 5:** Config Generation - Generate openclaw.json fragments, tool policies, memory config, failover, heartbeat, logging
**Step 6:** Self-Correction - Generate REVIEW.md and self-correction directives per agent
**Step 7:** Assembly - Assemble complete workspace directory structure
**Step 8:** Review - Present generated workspace for user review and refinement

### Output / Deliverable

A complete workspace directory at `{ocf_output_folder}/{system-name}/` containing:
- Per-agent: AGENTS.md, SOUL.md, USER.md, MEMORY.md, skills/, REVIEW.md
- System-level: openclaw.json fragments, tool policies, memory config, failover config, heartbeat config, logging config

### Input Requirements

- **Required:** Structured agent system brief (from create-agent-brief workflow)
- **Optional:** Existing OpenClaw configuration for reference; custom templates or overrides

### Key Instructions to LLM

- Spec assigns primary agents: Anima (Soul Smith) leads identity generation, Cog (Gear Wright) leads config and assembly
- Vulcan (Forge Master) provides architecture context from the brief
- The workflow is create-only (steps-c/ only, no tri-modal)
- Document-producing workflow — all output is file artifacts
- Web bundle enabled

---

## Conversion Notes

**What works well in original:**
- Clear 8-step decomposition with distinct responsibilities
- Well-defined input/output contract
- Agent role assignments are specific and purposeful
- Logical ordering: identity first, then context, skills, config, self-correction, assembly, review

**What needs improvement:**
- Spec is a placeholder — no actual step files, templates, or execution logic exist
- No menus, user interaction points, or YOLO mode considerations defined
- No state tracking or frontmatter management specified
- No template references for the generated artifacts

**Compliance gaps identified:**
- No step files exist (steps-c/ directory empty or non-existent)
- No workflow.md entry point file
- No data/ or templates/ directory
- No MANDATORY EXECUTION RULES or EXECUTION PROTOCOLS per step
- No menu handling logic defined
- No frontmatter state tracking implemented

---

## Classification Decisions

**Workflow Name:** create-agent-system
**Target Path:** {project-root}/_bmad/ocf/workflows/create-agent-system/

**4 Key Decisions:**
1. **Document Output:** true (multi-document-producing — generates AGENTS.md, SOUL.md, USER.md, MEMORY.md, REVIEW.md, openclaw.json fragments per agent)
2. **Module Affiliation:** OCF module (stored in _bmad/ocf/workflows/)
3. **Session Type:** Continuable (multi-session — 8 steps generating artifacts for potentially many agents, high token consumption)
4. **Lifecycle Support:** Create-only (steps-c/ only — each run generates fresh workspace from brief)

**Structure Implications:**
- Needs steps-c/ directory with step files
- Needs step-01-init.md with continuation detection and step-01b-continue.md for resuming
- Needs stepsCompleted tracking in output frontmatter
- Needs data/ directory for shared reference data (OCF artifact templates, schema definitions)
- No steps-e/ or steps-v/ needed
- Web bundle enabled

---

## Requirements

**Flow Structure:**
- Pattern: Linear (8 sequential steps)
- Phases: Load & Validate → Identity Generation → Context Generation → Skill Generation → Config Generation → Self-Correction → Assembly → Review
- Estimated steps: 10 step files (8 core + step-01b-continue + step-01-init replaces step-01)

**User Interaction:**
- Style: Mixed (mostly autonomous generation with collaborative review at end)
- Decision points: Step 1 (brief selection/validation), Step 8 (review and refinement approval)
- Checkpoint frequency: Menu at end of each step for YOLO/continue; Step 8 is a full interactive review
- YOLO support: Steps 2-7 should support autonomous generation without pausing

**Inputs Required:**
- Required: Structured agent system brief (output of create-agent-brief workflow)
- Optional: Existing OpenClaw configuration for reference, custom templates or overrides
- Prerequisites: create-agent-brief workflow must have been run first

**Output Specifications:**
- Type: Multi-document (many files in a directory structure)
- Format: Structured (each artifact type follows OCF schema definitions)
- Output pattern: Plan-then-build — steps 1-6 generate artifacts progressively into a workspace plan, step 7 assembles final directory
- Output location: {ocf_output_folder}/{system-name}/
- Per-agent artifacts: AGENTS.md, SOUL.md, USER.md, MEMORY.md, skills/ (with SKILL.md files), REVIEW.md
- System-level artifacts: openclaw.json fragments, tool policies, memory config, failover config, heartbeat config, logging config

**Success Criteria:**
- Every agent from the brief has a complete set of artifacts (SOUL.md, AGENTS.md, USER.md, MEMORY.md, skills/, REVIEW.md)
- All system-level config files are generated and internally consistent
- Directory structure matches OCF workspace conventions
- openclaw.json fragments are valid and reference correct paths
- User has reviewed and approved the generated workspace

**Instruction Style:**
- Overall: Mixed
- Generation steps (2-6): Prescriptive — follow OCF artifact schemas and conventions strictly
- Assembly step (7): Prescriptive — follow directory structure conventions
- Review step (8): Intent-based — facilitate collaborative review and refinement
- Notes: Agent role context (Anima, Cog, Vulcan) should be injected into relevant step preambles

---

## Design Preview

**Phase 1: Initialization & Brief Loading**
- Welcome user, detect continuation (step-01b-continue if resuming)
- Load and validate the agent system brief
- Extract agent list, system name, architecture context
- Create output workspace plan document

**Phase 2: Identity Generation (Anima)**
- For each agent: generate SOUL.md (persona, voice, principles)
- For each agent: generate AGENTS.md (role, capabilities, boundaries)

**Phase 3: Context Generation**
- For each agent: generate USER.md templates
- For each agent: generate MEMORY.md scaffolds

**Phase 4: Skill Generation**
- For each agent: generate skills/ directory structure
- For each agent: generate SKILL.md files

**Phase 5: Config Generation (Cog)**
- Generate openclaw.json fragments per agent
- Generate tool policies, memory config, failover, heartbeat, logging

**Phase 6: Self-Correction**
- For each agent: generate REVIEW.md
- For each agent: generate self-correction directives

**Phase 7: Assembly**
- Create complete workspace directory structure
- Place all generated artifacts in correct locations

**Phase 8: Review**
- Present complete workspace to user
- Interactive review and refinement cycle

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** Excluded — generation workflow, no creative brainstorming needed
- **Advanced Elicitation:** Excluded — inputs come from structured brief, not user discovery
- **Brainstorming:** Excluded — no ideation phases in this workflow

**LLM Features:**
- **Web-Browsing:** Excluded — all content derived from brief and OCF schemas
- **File I/O:** Included — critical for reading brief input and writing all output artifacts to workspace directory
- **Sub-Agents:** Excluded — linear sequential generation, no parallel specialization needed
- **Sub-Processes:** Excluded — sequential step execution

**Memory:**
- Type: Continuable (multi-session)
- Tracking: stepsCompleted array, lastStep, lastContinued date in workspace plan frontmatter
- Sidecar: Track which agents have been fully processed (agentsCompleted array)

**External Integrations:**
- None required — all operations are local file generation from brief input

**Installation Requirements:**
- None — all tools are built-in BMAD capabilities

---

## Workflow Structure Design

### File Structure

```
create-agent-system/
├── workflow.md                          # Entry point
├── data/
│   ├── ocf-artifact-schemas.md          # Schema definitions for all OCF artifacts
│   └── workspace-directory-structure.md # Standard workspace directory layout
└── steps-c/
    ├── step-01-init.md                  # Initialize, discover brief, create workspace plan
    ├── step-01b-continue.md             # Resume interrupted workflow
    ├── step-02-identity.md              # Generate SOUL.md and AGENTS.md per agent
    ├── step-03-context.md               # Generate USER.md and MEMORY.md per agent
    ├── step-04-skills.md                # Generate skills/ directory and SKILL.md per agent
    ├── step-05-config.md                # Generate openclaw.json, tool policies, memory, failover, heartbeat, logging
    ├── step-06-self-correction.md       # Generate REVIEW.md and self-correction directives per agent
    ├── step-07-assembly.md              # Assemble workspace directory structure with all artifacts
    └── step-08-review.md               # Present workspace for user review and refinement (final step)
```

### Step Sequence Design

#### Step 01: Init (Continuable, With Input Discovery)

**Type:** Init (Continuable + Input Discovery)
**Goal:** Discover the agent system brief, validate it, extract agent roster and system name, create the workspace plan document.
**Menu:** C only (auto-proceed after discovery)

**Frontmatter variables:**
- `continueFile: './step-01b-continue.md'`
- `nextStepFile: './step-02-identity.md'`
- `outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'`
- `inputFilePatterns: ['agent-brief-*.md']`
- `moduleInputFolder: '{ocf_output_folder}/briefs'`

**Sequence:**
1. Check for existing workspace-plan.md → if exists with stepsCompleted, route to step-01b-continue
2. Discover agent brief in `{ocf_output_folder}/briefs/` using pattern `agent-brief-*.md`
3. Present found briefs, user selects one
4. Load and validate the brief — extract: system name, agent roster (names, roles), architecture context
5. Create workspace plan document at `{outputFile}` with extracted data
6. Display summary of what will be generated, auto-proceed to step 02

**Data flow OUT:** workspace-plan.md containing system_name, agent_roster[], architecture_context

---

#### Step 01b: Continue

**Type:** Continuation
**Goal:** Resume interrupted workflow from last completed step.

**Frontmatter variables:**
- `outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'`

**Sequence:**
1. Read workspace-plan.md frontmatter (stepsCompleted, lastStep)
2. Read last completed step file to find its nextStepFile
3. Welcome user back, show progress summary
4. Route to next uncompleted step

---

#### Step 02: Identity Generation (Anima Phase)

**Type:** Middle (Standard)
**Goal:** Generate SOUL.md and AGENTS.md for each agent defined in the brief.
**Agent Role:** Anima (Soul Smith) — identity and persona expert
**Menu:** A/P/C (content can benefit from elicitation/party mode review)

**Frontmatter variables:**
- `nextStepFile: './step-03-context.md'`
- `outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'`
- `artifactSchemas: '../data/ocf-artifact-schemas.md'`
- `advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'`
- `partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'`

**Sequence:**
1. Load workspace-plan.md, extract agent roster
2. Load artifact schemas for SOUL.md and AGENTS.md formats
3. For each agent in roster:
   a. Generate SOUL.md content (persona, voice, principles, communication style)
   b. Generate AGENTS.md content (role definition, capabilities, boundaries, relationships)
   c. Append generated content to workspace-plan.md under agent section
4. Present summary of generated identities
5. Menu: A/P/C

**Data flow IN:** agent_roster, architecture_context from workspace-plan
**Data flow OUT:** SOUL.md and AGENTS.md content per agent appended to workspace-plan

**Subprocess opportunity:** Pattern 2 — for large agent rosters, launch subprocess per agent to generate identity artifacts

---

#### Step 03: Context Generation

**Type:** Middle (Standard)
**Goal:** Generate USER.md templates and MEMORY.md scaffolds for each agent.
**Menu:** A/P/C

**Frontmatter variables:**
- `nextStepFile: './step-04-skills.md'`
- `outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'`
- `artifactSchemas: '../data/ocf-artifact-schemas.md'`
- `advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'`
- `partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'`

**Sequence:**
1. Load workspace-plan.md, extract agent roster and identity context
2. Load artifact schemas for USER.md and MEMORY.md formats
3. For each agent:
   a. Generate USER.md template (user context sections, placeholders for runtime data)
   b. Generate MEMORY.md scaffold (memory categories, retention rules, context management)
   c. Append to workspace-plan.md
4. Present summary
5. Menu: A/P/C

**Subprocess opportunity:** Pattern 2 — per-agent generation

---

#### Step 04: Skill Generation

**Type:** Middle (Standard)
**Goal:** Generate skills/ directory structure and SKILL.md files for each agent.
**Menu:** A/P/C

**Frontmatter variables:**
- `nextStepFile: './step-05-config.md'`
- `outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'`
- `artifactSchemas: '../data/ocf-artifact-schemas.md'`
- `advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'`
- `partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'`

**Sequence:**
1. Load workspace-plan.md, extract agent roster with identity and context info
2. Load artifact schemas for SKILL.md format
3. For each agent:
   a. Determine skills from brief (skill & channel mapping section)
   b. Generate SKILL.md for each skill (description, gating rules, invocation patterns)
   c. Append skill listing to workspace-plan.md
4. Present summary of generated skills per agent
5. Menu: A/P/C

**Subprocess opportunity:** Pattern 2 — per-agent skill generation

---

#### Step 05: Config Generation (Cog Phase)

**Type:** Middle (Standard)
**Goal:** Generate openclaw.json fragments, tool policies, memory config, failover config, heartbeat config, and logging config.
**Agent Role:** Cog (Gear Wright) — configuration and systems expert
**Menu:** A/P/C

**Frontmatter variables:**
- `nextStepFile: './step-06-self-correction.md'`
- `outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'`
- `artifactSchemas: '../data/ocf-artifact-schemas.md'`
- `advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'`
- `partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'`

**Sequence:**
1. Load workspace-plan.md, extract all agent data generated so far
2. Load artifact schemas for config file formats
3. For each agent: generate openclaw.json fragment (model, tools, permissions, memory references)
4. Generate system-level configs:
   a. Tool policies (allowed/denied tools per agent)
   b. Memory config (memory architecture from brief's Memory & Resilience section)
   c. Failover config (fallback behaviors, error handling)
   d. Heartbeat config (monitoring, health checks)
   e. Logging config (log levels, destinations)
5. Append all config content to workspace-plan.md
6. Present summary
7. Menu: A/P/C

---

#### Step 06: Self-Correction Generation

**Type:** Middle (Standard)
**Goal:** Generate REVIEW.md and self-correction directives for each agent.
**Menu:** A/P/C

**Frontmatter variables:**
- `nextStepFile: './step-07-assembly.md'`
- `outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'`
- `artifactSchemas: '../data/ocf-artifact-schemas.md'`
- `advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'`
- `partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'`

**Sequence:**
1. Load workspace-plan.md, extract agent data
2. Load artifact schemas for REVIEW.md format
3. For each agent:
   a. Generate REVIEW.md (review criteria, quality gates, self-assessment checklist)
   b. Generate self-correction directives (error detection, recovery patterns)
   c. Append to workspace-plan.md
4. Present summary
5. Menu: A/P/C

---

#### Step 07: Assembly

**Type:** Middle (Simple) — autonomous file writing
**Goal:** Read workspace-plan.md and assemble the complete workspace directory structure by writing all artifact files to disk.
**Agent Role:** Cog (Gear Wright) — assembly and structure expert
**Menu:** C only (auto-proceed after assembly)

**Frontmatter variables:**
- `nextStepFile: './step-08-review.md'`
- `outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'`
- `directoryStructure: '../data/workspace-directory-structure.md'`

**Sequence:**
1. Load workspace-plan.md completely — all generated content
2. Load workspace-directory-structure.md for standard layout
3. Create directory structure:
   ```
   {ocf_output_folder}/{system-name}/
   ├── agents/
   │   ├── {agent-1}/
   │   │   ├── AGENTS.md
   │   │   ├── SOUL.md
   │   │   ├── USER.md
   │   │   ├── MEMORY.md
   │   │   ├── REVIEW.md
   │   │   └── skills/
   │   │       ├── SKILL-1.md
   │   │       └── SKILL-N.md
   │   └── {agent-N}/
   │       └── ... (same structure)
   ├── config/
   │   ├── openclaw.json
   │   ├── tool-policies.json
   │   ├── memory-config.json
   │   ├── failover-config.json
   │   ├── heartbeat-config.json
   │   └── logging-config.json
   └── workspace-plan.md
   ```
4. Write each artifact file from workspace-plan.md content to its target path
5. Update workspace-plan.md frontmatter: mark assembly complete, record file manifest
6. Present assembly summary with file count
7. Menu: C only

---

#### Step 08: Review (Final Step)

**Type:** Final Step
**Goal:** Present the complete generated workspace for user review and refinement.
**Menu:** Custom (Review/Refine/Accept)
**No nextStepFile** — this is the final step.

**Frontmatter variables:**
- `outputFile: '{ocf_output_folder}/{system_name}/workspace-plan.md'`
- `advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'`
- `partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'`

**Sequence:**
1. Load workspace-plan.md, read file manifest from assembly step
2. Present workspace overview:
   - System name and agent count
   - Per-agent artifact summary (list each file generated)
   - System-level config summary
   - Total file count and directory structure
3. Ask user to review specific agents or areas of concern
4. For any refinement requests:
   a. Load the specific artifact file
   b. Apply user-requested changes
   c. Save updated file
   d. Loop back to review
5. Menu: [R] Review Agent [E] Edit Artifact [A] Advanced Elicitation [P] Party Mode [D] Done
   - R: User selects agent to review, present all artifacts for that agent
   - E: User specifies file to edit, load and present for modification
   - A: Execute advanced elicitation for quality review
   - P: Execute party mode for multi-perspective review
   - D: Mark workspace as complete, update frontmatter, end workflow

---

### Interaction Patterns

| Step | Menu Pattern | Interaction Style |
|------|-------------|-------------------|
| 01 | C only (auto-proceed) | Autonomous with brief selection |
| 01b | Auto-route | Autonomous continuation |
| 02 | A/P/C | Prescriptive generation, optional review |
| 03 | A/P/C | Prescriptive generation, optional review |
| 04 | A/P/C | Prescriptive generation, optional review |
| 05 | A/P/C | Prescriptive generation, optional review |
| 06 | A/P/C | Prescriptive generation, optional review |
| 07 | C only | Autonomous assembly |
| 08 | Custom R/E/A/P/D | Collaborative review |

### Data Flow

```
Brief (input) → Step 01 → workspace-plan.md (created)
                           ↓
Step 02 → workspace-plan.md (+ identity content per agent)
                           ↓
Step 03 → workspace-plan.md (+ context content per agent)
                           ↓
Step 04 → workspace-plan.md (+ skills content per agent)
                           ↓
Step 05 → workspace-plan.md (+ config content)
                           ↓
Step 06 → workspace-plan.md (+ self-correction content per agent)
                           ↓
Step 07 → workspace-plan.md → writes individual files to disk
                           ↓
Step 08 → review & refine individual files
```

### Role and Persona Definition

- **Primary workflow role:** OpenClaw Workspace Generator
- **Tone:** Technical, precise, systematic
- **Communication:** Progress-oriented — report what was generated, summarize counts, show structure
- **Agent roles per step:**
  - Steps 02-03: Adopt Anima (Soul Smith) perspective — focus on identity, persona, communication style
  - Steps 05, 07: Adopt Cog (Gear Wright) perspective — focus on configuration, structure, systems
  - Steps 04, 06: Neutral technical perspective
  - Step 08: Collaborative reviewer

### Subprocess Optimization

**Steps 02-06:** Pattern 2 (per-agent deep analysis/generation)
- For agent rosters > 3 agents, launch subprocess per agent
- Each subprocess receives: agent brief data, artifact schema, previous artifacts for context
- Each subprocess returns: generated artifact content (structured markdown)
- Fallback: sequential generation in main thread

### Workflow Chaining

- **Input from:** create-agent-brief workflow → `{ocf_output_folder}/briefs/agent-brief-{system-name}.md`
- **Output to:** edit-agent-system, validate-workspace, configure-production-hardening, export-config workflows
- **Chaining note:** Output workspace at `{ocf_output_folder}/{system-name}/` is the standard input path for downstream OCF workflows
