---
conversionFrom: 'src/modules/ocf/workflows/package-import/package-import.spec.md'
originalFormat: 'BMAD spec placeholder'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design']
created: 2026-02-11
status: APPROVED_FOR_DESIGN
approvedDate: 2026-02-11
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/ocf/workflows/package-import/package-import.spec.md
**Original Format:** BMAD spec placeholder (not a full workflow — a specification document)
**Detected Structure:** 5-step utility workflow spec for receiving and installing OCF packages

---

## Original Workflow Analysis

### Goal (from source)

Receive an .ocf.zip + setup prompt and execute the installation on a running OpenClaw instance.

### Original Steps (Complete List)

**Step 1:** Receive Package - Accept and validate the .ocf.zip archive
**Step 2:** Extract - Unpack workspace files to target directories
**Step 3:** Configure - Merge openclaw.json fragments into existing configuration
**Step 4:** Register - Register agent entries and set up bindings
**Step 5:** Activate - Bring the new agent system online and verify

### Output / Deliverable

- Installed workspace files in target directories
- Merged openclaw.json configuration
- Installation report

### Input Requirements

- .ocf.zip archive
- setup.md prompt (companion to the archive)
- Optional: target installation directory, configuration overrides

### Key Instructions to LLM

The spec describes Cog (Gear Wright) as the primary agent — assembly and installation specialist. The workflow is create-only, non-document producing (it performs actions), and utility-type.

---

## Conversion Notes

**What works well in original:**
- Clear 5-step decomposition
- Well-defined inputs/outputs
- Logical flow from receive -> extract -> configure -> register -> activate

**What needs improvement:**
- No actual step files exist — only a placeholder spec
- Need to design the actual execution logic
- Need to handle error cases (invalid archive, merge conflicts, missing dependencies)

**Compliance gaps identified:**
- No workflow.md
- No step files
- No data files or templates
- No BMAD step-file architecture

---

## Classification Decisions

**Workflow Name:** package-import
**Target Path:** {project-root}/src/modules/ocf/workflows/package-import

**4 Key Decisions:**
1. **Document Output:** true (produces installation report)
2. **Module Affiliation:** OCF module
3. **Session Type:** single-session
4. **Lifecycle Support:** create-only (steps-c/ only)

**Structure Implications:**
- Needs steps-c/ only (create-only)
- No step-01b-continue.md needed (single-session)
- Produces an installation report document
- OCF module variables available

---

## Requirements

**Flow Structure:**
- Pattern: linear (step 1 -> 2 -> 3 -> 4 -> 5)
- Phases: Receive, Extract, Configure, Register, Report
- Estimated steps: 5

**User Interaction:**
- Style: mostly autonomous with checkpoints
- Decision points: step 1 (validate archive before proceeding), step 3 (confirm merge strategy for conflicts)
- Checkpoint frequency: pause at validation and conflict resolution only

**Inputs Required:**
- Required: .ocf.zip archive path, setup.md prompt path
- Optional: target installation directory, configuration overrides
- Prerequisites: running OpenClaw instance with existing openclaw.json

**Output Specifications:**
- Type: document (installation report) + action (files installed)
- Format: structured report
- Sections: Package Info, Extraction Summary, Configuration Changes, Registration, Activation Status

**Success Criteria:**
- All workspace files extracted to correct directories
- openclaw.json configuration merged without data loss
- Agent entries registered
- Bindings set up correctly
- Installation report generated with pass/fail status

**Instruction Style:**
- Overall: mixed (prescriptive for file operations, intent-based for conflict resolution)
- Notes: File I/O operations must be precise; user interaction for conflict resolution should be collaborative

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** excluded - not applicable for utility workflow
- **Advanced Elicitation:** excluded - not applicable for utility workflow
- **Brainstorming:** excluded - not applicable for utility workflow

**LLM Features:**
- **Web-Browsing:** excluded - local operation only
- **File I/O:** included - core requirement for extraction, merging, and installation
- **Sub-Agents:** excluded - single agent workflow
- **Sub-Processes:** excluded - sequential operations

**Memory:**
- Type: single-session
- Tracking: none needed

**External Integrations:**
- None

**Installation Requirements:**
- None beyond standard file I/O

---

## Workflow Design

### Step Sequence

**Step 01: Receive and Validate Package**
- Type: Init (Non-Continuable)
- Goal: Accept the .ocf.zip archive path and setup.md path, validate both exist and are well-formed
- Actions:
  1. Get archive path from user (or argument)
  2. Get setup.md path from user (or argument)
  3. Validate .ocf.zip exists
  4. Read and parse setup.md for installation instructions
  5. Initialize installation report from template
  6. Present package summary and auto-proceed
- Menu: Auto-proceed after validation
- Subprocess: none

**Step 02: Extract Package**
- Type: Validation Sequence (auto-proceed)
- Goal: Unpack workspace files from the archive to target directories
- Actions:
  1. Determine target workspace directory (from setup.md or user input)
  2. List archive contents
  3. Extract workspace files to target directory
  4. Verify extraction (file count, structure)
  5. Record extraction results in report
  6. Auto-proceed to configuration
- Menu: Auto-proceed
- Subprocess: none

**Step 03: Configure**
- Type: Middle (Simple) - C only menu
- Goal: Merge openclaw.json configuration fragments from the package into existing configuration
- Actions:
  1. Read existing openclaw.json
  2. Read package's openclaw.json fragment/overlay
  3. Identify merge points (agents, bindings, models, tools)
  4. Detect conflicts
  5. If conflicts: present to user for resolution
  6. Perform merge
  7. Record configuration changes in report
- Menu: C only (pause for conflict review if needed)
- Subprocess: none

**Step 04: Register and Activate**
- Type: Validation Sequence (auto-proceed)
- Goal: Register agent entries, set up bindings, and verify the system is active
- Actions:
  1. Register agent entries from merged config
  2. Set up channel bindings
  3. Verify workspace file references resolve
  4. Record registration results in report
  5. Auto-proceed to final report
- Menu: Auto-proceed
- Subprocess: none

**Step 05: Installation Report**
- Type: Final Step
- Goal: Compile and present the installation report with pass/fail status
- Actions:
  1. Compile overall status from all steps
  2. Generate recommendations for any issues
  3. Present final report to user
  4. Save report to output
- Menu: Final (D for done, R for read report)
- Subprocess: none

### Data Flow

- Step 01 creates: report file, parsed setup.md instructions
- Step 02 reads: setup.md instructions; creates: extracted files
- Step 03 reads: existing openclaw.json + package overlay; creates: merged config
- Step 04 reads: merged config; creates: registered entries
- Step 05 reads: all step results from report; creates: final report

### File Structure

```
package-import/
├── workflow.md
├── steps-c/
│   ├── step-01-receive.md
│   ├── step-02-extract.md
│   ├── step-03-configure.md
│   ├── step-04-register.md
│   └── step-05-report.md
├── data/
│   └── installation-checklist.md
└── templates/
    └── installation-report-template.md
```

### Role and Persona

- Role: Installation specialist (Cog / Gear Wright)
- Tone: Systematic, precise, methodical
- Expertise: Package management, configuration merging, workspace architecture
- Collaborative for: conflict resolution during merge
- Autonomous for: extraction, validation, registration

---

## Foundation Build Complete

**To be created:**
- Folder structure at: {project-root}/src/modules/ocf/workflows/package-import
- workflow.md
- Main template: installation-report-template.md
- Data: installation-checklist.md
