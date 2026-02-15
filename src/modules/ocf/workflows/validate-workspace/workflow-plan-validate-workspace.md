---
conversionFrom: 'src/modules/ocf/workflows/validate-workspace/validate-workspace.spec.md'
originalFormat: 'OCF Workflow Specification (.spec.md)'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-all-steps', 'step-10-confirmation']
created: 2026-02-11
status: COMPLETE
approvedDate: 2026-02-11
completedDate: 2026-02-11
---

# Workflow Creation Plan: validate-workspace

## Conversion Source

**Original Path:** src/modules/ocf/workflows/validate-workspace/validate-workspace.spec.md
**Original Format:** OCF Workflow Specification (.spec.md)
**Detected Structure:** 5-step validation utility workflow for OpenClaw agent workspaces. Create-only mode, document-producing (validation report).

---

## Classification Decisions

**Workflow Name:** validate-workspace
**Target Path:** src/modules/ocf/workflows/validate-workspace/

**4 Key Decisions:**
1. **Document Output:** true (produces a validation report)
2. **Module Affiliation:** OCF module (OpenClaw Forge)
3. **Session Type:** single-session (validation runs are quick, auto-proceed)
4. **Lifecycle Support:** create-only (steps-c/ only — this IS the validator)

---

## Requirements

**Flow Structure:**
- Pattern: linear with auto-proceed
- Phases: Load → Structural → Coherence → Hardening → Report
- Estimated steps: 5 steps

**User Interaction:**
- Style: mostly autonomous (auto-proceed through validation checks)
- Decision points: Step 1 (workspace path input, optional check selection), Step 5 (report review and next actions)
- Checkpoint frequency: only at start (input) and end (report)

**Inputs Required:**
- Required: Path to OpenClaw workspace directory
- Optional: Specific check categories to run (structural, coherence, hardening, or all)
- Prerequisites: Workspace must exist with at least some artifacts generated

**Output Specifications:**
- Type: document (validation report)
- Format: structured (defined sections per check category)
- Sections: Header/metadata, Structural Checks, Coherence Checks, Hardening Checks, Summary
- Frequency: single report per run

**Instruction Style:**
- Overall: prescriptive (validation checks are systematic, not creative)
- Auto-proceed between validation steps 02-04. User interaction at step 01 and step 05 only.

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** excluded — validation is systematic, not creative
- **Advanced Elicitation:** excluded — no collaborative brainstorming needed
- **Brainstorming:** excluded — not applicable

**LLM Features:**
- **File I/O:** included — must read workspace files (SOUL.md, AGENTS.md, etc.) and openclaw.json
- **Web-Browsing:** excluded — no external data needed
- **Sub-Agents:** excluded — not needed for this scope
- **Sub-Processes:** excluded — sequential validation is sufficient

**Memory:**
- Type: single-session
- Tracking: none (no stepsCompleted needed — single-session auto-proceed)

**External Integrations:** None

**Installation Requirements:** None

---

## Workflow Design

### File Structure

```
src/modules/ocf/workflows/validate-workspace/
├── workflow.md                        # Entry point
├── steps-c/
│   ├── step-01-load-workspace.md      # Get workspace path, inventory artifacts
│   ├── step-02-structural-checks.md   # File presence and well-formedness
│   ├── step-03-coherence-checks.md    # Cross-artifact consistency
│   ├── step-04-hardening-checks.md    # Security and resilience
│   └── step-05-report.md             # Generate final report with summary
├── data/
│   └── workspace-validation-rules.md  # Reference: all validation rules
└── templates/
    └── validation-report-template.md  # Output template for the report
```

### Step Design

**Step 01: Load Workspace** (Init step, user interaction)
- Type: Init Step (Non-Continuable)
- Goal: Get workspace path from user, inventory all artifacts, initialize validation report
- Actions:
  1. Ask user for workspace path
  2. Ask which checks to run (all / structural / coherence / hardening)
  3. Load and list all files found in the workspace
  4. Create validation report from template
  5. Auto-proceed to step 02
- Menu: Auto-proceed after initialization
- Outputs: Initialized validation report with workspace inventory

**Step 02: Structural Checks** (Validation step, auto-proceed)
- Type: Validation Sequence Step
- Goal: Verify all required files exist and are well-formed
- Actions:
  1. Load workspace-validation-rules.md for structural check criteria
  2. Check each required file (SOUL.md, AGENTS.md, USER.md, etc.)
  3. Check each optional file with warnings
  4. Check directory structure (memory/, skills/)
  5. Check BOOTSTRAP.md absence
  6. Append findings to validation report
  7. Auto-proceed to step 03
- Menu: Auto-proceed (no user interaction)
- Outputs: Structural Checks section of report

**Step 03: Coherence Checks** (Validation step, auto-proceed)
- Type: Validation Sequence Step
- Goal: Validate cross-artifact consistency
- Actions:
  1. Load workspace-validation-rules.md for coherence check criteria
  2. Read SOUL.md and AGENTS.md to check personality/directive consistency
  3. Verify AGENTS.md session startup references (SOUL.md, USER.md, memory)
  4. Check skill references vs actual skill directories
  5. Verify binding completeness if openclaw.json exists
  6. Check IDENTITY.md consistency with SOUL.md
  7. Append findings to validation report
  8. Auto-proceed to step 04
- Menu: Auto-proceed (no user interaction)
- Outputs: Coherence Checks section of report

**Step 04: Hardening Checks** (Validation step, auto-proceed)
- Type: Validation Sequence Step
- Goal: Verify security, resilience, and operational hardening
- Actions:
  1. Load workspace-validation-rules.md for hardening check criteria
  2. Check memory directives in AGENTS.md
  3. Check memory backend config in openclaw.json
  4. Check tool policies
  5. Check boundaries in SOUL.md
  6. Check failover configuration
  7. Check self-correction directives
  8. Check safety section in AGENTS.md
  9. Append findings to validation report
  10. Auto-proceed to step 05
- Menu: Auto-proceed (no user interaction)
- Outputs: Hardening Checks section of report

**Step 05: Report** (Final step, user interaction)
- Type: Final Step
- Goal: Compile overall status, present report, offer next actions
- Actions:
  1. Calculate overall status (PASS/WARNINGS/FAIL)
  2. Count pass/fail/warning totals
  3. Generate recommendations from failures and warnings
  4. Append summary section to validation report
  5. Present report to user
  6. Offer next actions menu
- Menu: Custom menu [R] Read full report [F] Fix issues [D] Done
- Outputs: Completed validation report

### Data Flow

```
User provides workspace path
    ↓
Step 01: Inventory artifacts → Initialize report
    ↓ (auto-proceed)
Step 02: Read files → Structural checks → Append to report
    ↓ (auto-proceed)
Step 03: Read + cross-reference → Coherence checks → Append to report
    ↓ (auto-proceed)
Step 04: Read + verify → Hardening checks → Append to report
    ↓ (auto-proceed)
Step 05: Compile summary → Present report → User actions
```

### Role Definition

- **Role:** Configuration validation specialist (Cog / Gear Wright)
- **Tone:** Systematic, thorough, objective — reports facts, not opinions
- **Style:** Prescriptive validation sequence with auto-proceed
- **Expertise:** OpenClaw workspace architecture, agent configuration standards
