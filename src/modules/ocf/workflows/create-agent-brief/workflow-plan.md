---
conversionFrom: 'src/modules/ocf/workflows/create-agent-brief/create-agent-brief.spec.md'
originalFormat: 'BMAD Workflow Specification (spec.md)'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-all-steps']
created: 2026-02-11
status: BUILD_COMPLETE
approvedDate: 2026-02-11
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/ocf/workflows/create-agent-brief/create-agent-brief.spec.md
**Original Format:** BMAD Workflow Specification (spec.md — placeholder, not yet implemented)
**Detected Structure:** Single spec file defining a 6-step create-only workflow for guided agent system discovery

---

## Original Workflow Analysis

### Goal (from source)

Guide users through structured discovery of a new OpenClaw agent system (single or multi-agent). Produces a structured brief covering all aspects: agents, personas, skills, channels, orchestration, memory architecture, resilience needs, and safety requirements.

### Original Steps (Complete List)

**Step 1:** Concept Gathering - Capture the user's agent system idea and high-level goals
**Step 2:** Agent Roster Design - Define agents, their roles, personas, and responsibilities
**Step 3:** Skill & Channel Mapping - Identify skills, tools, and channel bindings per agent
**Step 4:** Orchestration Planning - Design multi-agent communication, routing, and handoff patterns
**Step 5:** Memory & Resilience - Plan memory architecture, self-correction, failover, and safety
**Step 6:** Brief Assembly - Compile all gathered information into the structured brief document

### Output / Deliverable

Document-producing workflow generating `{ocf_output_folder}/briefs/agent-brief-{system-name}.md` — a structured agent system brief document.

### Input Requirements

- **Required:** User's agent system concept/idea (gathered through conversation)
- **Optional:** Existing OpenClaw workspace for reference
- **Optional:** Channel requirements (WhatsApp, Telegram, Discord, etc.)

### Key Instructions to LLM

- Led by Vulcan (Forge Master) agent persona
- Collaborative guided discovery approach — conversation-driven
- Entry-point workflow before handoff to other agents/workflows
- Create-only mode (steps-c/ only, no tri-modal)

---

## Conversion Notes

**What works well in original:**
- Clear 6-step progression from concept to deliverable
- Logical funnel: broad concept → specific architecture → compiled output
- Well-defined output path and format
- Agent assignment (Vulcan) is specified

**What needs improvement:**
- Spec is a placeholder — no actual step files, templates, or workflow.md exist
- No menu structures, continuation logic, or state tracking defined
- No template for the output brief document
- No detail on what questions to ask at each step

**Compliance gaps identified:**
- No workflow.md entry point
- No step files in steps-c/
- No frontmatter with BMAD workflow metadata
- No sequential enforcement or menu handling
- No state tracking via stepsCompleted
- No output template defined

---

## Classification Decisions

**Workflow Name:** create-agent-brief
**Target Path:** {project-root}/_bmad/ocf/workflows/create-agent-brief/

**4 Key Decisions:**
1. **Document Output:** true
2. **Module Affiliation:** OCF (OpenClaw Framework)
3. **Session Type:** continuable
4. **Lifecycle Support:** create-only

**Structure Implications:**
- Needs `steps-c/` folder only (create-only, no tri-modal)
- Needs `step-01-init.md` with continuation detection
- Needs `step-01b-continue.md` for resuming
- Needs `stepsCompleted` tracking in output frontmatter
- Needs output template for the agent brief document
- Uses `data/` folder for shared reference data

---

## Requirements

**Flow Structure:**
- Pattern: Linear
- Phases: Concept Gathering → Agent Roster Design → Skill & Channel Mapping → Orchestration Planning → Memory & Resilience → Brief Assembly
- Estimated steps: 8 (init + continue + 6 content steps including final polish)

**User Interaction:**
- Style: Guided session / highly collaborative
- Decision points: Agent count, orchestration pattern selection, memory strategy choices
- Checkpoint frequency: End of each step with menu options
- Led by Vulcan (Forge Master) persona

**Inputs Required:**
- Required: User's agent system concept/idea (gathered conversationally)
- Optional: Existing OpenClaw workspace for reference
- Optional: Channel requirements (WhatsApp, Telegram, Discord, etc.)
- Prerequisites: None — this is the entry-point workflow

**Output Specifications:**
- Type: Document (structured agent brief)
- Format: Structured (defined sections mapping to discovery phases)
- Output pattern: Direct-to-final with final polish step
- Output path: `{ocf_output_folder}/briefs/agent-brief-{system-name}.md`
- Sections: System Overview, Agent Roster, Skills & Channels, Orchestration, Memory & Resilience, Safety Requirements

**Success Criteria:**
- Complete brief covering all 6 architecture areas
- Each agent has defined role, persona, and responsibilities
- Skills and channels mapped per agent
- Orchestration patterns clearly specified
- Memory and resilience strategy documented
- Safety requirements defined
- Brief is actionable for OpenClaw implementation

**Instruction Style:**
- Overall: Intent-based
- Notes: Creative/discovery facilitation — Vulcan guides through open-ended questions, adapting to user's domain and complexity level

---

## Workflow Structure Preview

**Phase 1: Initialization** — Welcome, continuation check, gather system name
**Phase 2: Concept Gathering** — Open-ended discovery of agent system idea and goals
**Phase 3: Agent Roster Design** — Define agents, roles, personas, responsibilities
**Phase 4: Skill & Channel Mapping** — Map skills, tools, channel bindings per agent
**Phase 5: Orchestration Planning** — Communication patterns, routing, handoff design
**Phase 6: Memory & Resilience** — Memory architecture, self-correction, failover, safety
**Phase 7: Brief Assembly & Polish** — Compile and polish final brief document

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** Excluded — workflow is already highly collaborative; would overcomplicate guided discovery
- **Advanced Elicitation:** Included — available at each step's menu for deeper exploration of complex decisions
- **Brainstorming:** Excluded — concept gathering step serves this purpose natively

**LLM Features:**
- **Web-Browsing:** Excluded — design/discovery workflow, not research
- **File I/O:** Included — reading existing OpenClaw workspaces (optional input) and writing output brief
- **Sub-Agents:** Excluded — single-agent guided workflow
- **Sub-Processes:** Excluded — linear flow, no parallelism needed

**Memory:**
- Type: Continuable
- Tracking: stepsCompleted, lastStep, lastContinued in output frontmatter

**External Integrations:**
- None required

**Installation Requirements:**
- None — all selected tools are built-in

---

## Workflow Design

### Step Sequence

| # | File | Type | Goal | Menu |
|---|------|------|------|------|
| 01 | `step-01-init.md` | Init (Continuable) | Welcome, check for existing brief, gather system name, create output doc | Auto-proceed |
| 01b | `step-01b-continue.md` | Continuation | Resume from previous session, route to last incomplete step | Auto-proceed |
| 02 | `step-02-concept.md` | Middle (Standard) | Capture agent system concept, domain, high-level goals, target users | A/P/C |
| 03 | `step-03-roster.md` | Middle (Standard) | Define agent roster: names, roles, personas, responsibilities | A/P/C |
| 04 | `step-04-skills.md` | Middle (Standard) | Map skills, tools, and channel bindings per agent | A/P/C |
| 05 | `step-05-orchestration.md` | Middle (Standard) | Design multi-agent communication, routing, handoff patterns | A/P/C |
| 06 | `step-06-resilience.md` | Middle (Standard) | Plan memory architecture, self-correction, failover, safety requirements | A/P/C |
| 07 | `step-07-assembly.md` | Final Polish + Final | Compile all sections, polish for coherence, finalize brief | C only |

### Data Flow

- **Output Pattern:** Direct-to-final
- Each step (02-06) facilitates conversation, then appends its section to the output brief
- Step 07 loads the complete document, polishes, and marks complete
- `stepsCompleted` updated in output frontmatter at each step transition

### File Structure

```
create-agent-brief/
├── workflow.md                    # Entry point
├── templates/
│   └── agent-brief.template.md   # Output document template
└── steps-c/
    ├── step-01-init.md            # Init with continuation detection
    ├── step-01b-continue.md       # Continuation handler
    ├── step-02-concept.md         # System concept gathering
    ├── step-03-roster.md          # Agent roster design
    ├── step-04-skills.md          # Skill & channel mapping
    ├── step-05-orchestration.md   # Orchestration planning
    ├── step-06-resilience.md      # Memory & resilience
    └── step-07-assembly.md        # Final assembly & polish
```

### Output Template Structure

```markdown
---
stepsCompleted: []
lastStep: ''
lastContinued: ''
date: ''
user_name: ''
system_name: ''
---

# Agent System Brief: {{system_name}}

## System Overview
[Appended by step-02-concept]

## Agent Roster
[Appended by step-03-roster]

## Skills & Channels
[Appended by step-04-skills]

## Orchestration
[Appended by step-05-orchestration]

## Memory & Resilience
[Appended by step-06-resilience]

## Safety Requirements
[Appended by step-06-resilience]
```

### Role & Persona

**Agent:** Vulcan (Forge Master)
**Expertise:** Workflow architecture, agent system design, OpenClaw framework
**Style:** Collaborative guided discovery, intent-based facilitation
**Tone:** Technical but approachable, asks open-ended questions, adapts to user's domain knowledge

### Subprocess Optimization

Not applicable — conversational discovery workflow with no file scanning, large data operations, or parallelizable analysis.

### Workflow Chaining

- **Before this workflow:** None (entry-point)
- **After this workflow:** OCF implementation workflows consume the output brief
- **Output consumed by:** Downstream agent creation, skill configuration, channel binding workflows
