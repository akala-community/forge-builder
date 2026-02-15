---
conversionFrom: 'src/modules/ocf/workflows/package-export/package-export.spec.md'
originalFormat: 'BMAD Workflow Spec (placeholder)'
stepsCompleted: ['step-00-conversion', 'step-02-classification', 'step-03-requirements', 'step-04-tools', 'step-05-plan-review', 'step-06-design', 'step-07-foundation', 'step-08-build-step-01', 'step-09-build-next-step', 'step-10-confirmation', 'step-11-completion']
created: 2026-02-11
completionDate: 2026-02-11
status: COMPLETE
approvedDate: 2026-02-11
---

# Workflow Creation Plan

## Conversion Source

**Original Path:** src/modules/ocf/workflows/package-export/package-export.spec.md
**Original Format:** BMAD Workflow Spec (placeholder)
**Detected Structure:** Single spec file describing a 4-step utility workflow. No existing step files, templates, or data files. The workflow is marked as "Placeholder -- To be created via create-workflow workflow."

---

## Original Workflow Analysis

### Goal (from source)

Bundle a completed workspace into a portable .zip archive + companion setup prompt. Takes a completed workspace and packages it into `{agent-system-name}.ocf.zip` containing all workspace files plus `{agent-system-name}.setup.md` with step-by-step instructions for an OpenClaw agent to unpack and activate the system. Includes OCF metadata for upgrade-path tracking.

### Original Steps (Complete List)

**Step 1:** Load Workspace - Load and validate workspace completeness
**Step 2:** Metadata Injection - Add OCF version and template metadata to artifacts
**Step 3:** Setup Prompt Generation - Generate setup.md with installation instructions
**Step 4:** Package Assembly - Bundle workspace + setup prompt into .ocf.zip

### Output / Deliverable

- `{ocf_output_folder}/packages/{system-name}.ocf.zip` -- Portable workspace archive
- `{ocf_output_folder}/packages/{system-name}.setup.md` -- Companion setup prompt

### Input Requirements

**Required:**
- Path to completed workspace

**Optional:**
- Custom setup instructions
- Target OpenClaw version

### Key Instructions to LLM

- Workflow type is Utility
- Create-only mode (steps-c/ only, no tri-modal)
- Primary agent: Cog (Gear Wright) -- assembly and packaging specialist
- Document-producing workflow
- web_bundle: true
- installed_path: '{project-root}/_bmad/ocf/workflows/package-export'

---

## Conversion Notes

**What works well in original:**
- Clear step breakdown with distinct responsibilities
- Well-defined inputs and outputs with naming conventions
- OCF metadata consideration for upgrade-path tracking
- Appropriate agent assignment (Cog for assembly/packaging)

**What needs improvement:**
- No actual step files exist -- everything needs to be created from scratch
- Step details are minimal (single-line goals only)
- No templates defined for setup.md output
- No validation or error handling patterns described

**Compliance gaps identified:**
- No step files (steps-c/ folder and step files need creation)
- No workflow.md entry point file
- No frontmatter with proper BMAD workflow metadata
- No menu/continuation patterns defined
- No execution protocols or mandatory rules per step
- No state tracking or stepsCompleted patterns

---

## Classification Decisions

**Workflow Name:** package-export
**Target Path:** src/modules/ocf/workflows/package-export/

**4 Key Decisions:**
1. **Document Output:** true (produces .ocf.zip archive + .setup.md companion prompt)
2. **Module Affiliation:** OCF (OpenClaw Forge module)
3. **Session Type:** single-session (utility workflow, 4 focused steps, low token consumption)
4. **Lifecycle Support:** create-only (steps-c/ only, per spec)

**Structure Implications:**
- Needs `steps-c/` folder only (no steps-e/ or steps-v/)
- No continuation logic (no step-01b-continue.md)
- Standard init step (no stepsCompleted tracking in output since single-session)
- Document-producing: generates setup.md via template, assembles zip
- Module variables available: `ocf_output_folder`, `user_name`, `communication_language`, `document_output_language`
- Installed path: `{project-root}/_bmad/ocf/workflows/package-export`

---

## Requirements

**Flow Structure:**
- Pattern: Linear (Load → Inject → Generate → Package)
- Phases: 4 distinct phases matching spec steps
- Estimated steps: 5 (init + 4 functional steps)

**User Interaction:**
- Style: Mostly autonomous with checkpoints
- Decision points: Workspace path confirmation (step 1), setup.md review before packaging (step 3→4 boundary)
- Checkpoint frequency: After workspace validation, after setup.md generation

**Inputs Required:**
- Required: Path to completed workspace (must contain AGENTS.md, openclaw.json, and other workspace artifacts)
- Optional: Custom setup instructions to include in setup.md, target OpenClaw version for metadata
- Prerequisites: Workspace must be "complete" (validated by validate-workspace workflow or manual confirmation)

**Output Specifications:**
- Type: Document + archive (dual output)
- Primary document: `{system-name}.setup.md` -- structured template with installation instructions
- Secondary artifact: `{system-name}.ocf.zip` -- zip archive containing workspace + setup.md
- Output location: `{ocf_output_folder}/packages/`
- Format: Structured template for setup.md (specific sections: system overview, prerequisites, unpacking steps, activation procedure, OCF metadata block)
- No final polish step needed -- setup.md is prescriptive, not prose

**Success Criteria:**
- Workspace loaded and validated as complete
- OCF version metadata injected into workspace artifacts
- setup.md generated with correct system name and complete installation instructions
- .ocf.zip created containing all workspace files + setup.md
- Archive is portable (no absolute paths, no environment-specific references)
- A receiving OpenClaw agent can follow setup.md to fully activate the system

**Instruction Style:**
- Overall: Prescriptive (packaging is mechanical/precise)
- Notes: Steps should provide exact file operations, not open-ended facilitation. The agent (Cog) is an engineer executing assembly tasks.

---

## Workflow Structure Preview

**Phase 1: Initialization**
- Get workspace path from user
- Validate workspace exists and contains required artifacts (AGENTS.md, openclaw.json, etc.)
- Extract system name from workspace
- Confirm packaging parameters

**Phase 2: Metadata Injection**
- Read current OCF version
- Inject OCF version metadata into workspace artifacts
- Add template origin tracking for upgrade paths
- Confirm metadata injection complete

**Phase 3: Setup Prompt Generation**
- Generate `{system-name}.setup.md` from structured template
- Include: system overview, prerequisites, unpacking steps, activation procedure, OCF metadata
- Include any custom setup instructions provided by user
- Present setup.md for review

**Phase 4: Package Assembly**
- Create `{ocf_output_folder}/packages/` directory if needed
- Bundle all workspace files + setup.md into `{system-name}.ocf.zip`
- Verify archive integrity
- Output final paths to user

---

## Tools Configuration

**Core BMAD Tools:**
- **Party Mode:** excluded - No creative exploration needed in utility packaging workflow
- **Advanced Elicitation:** excluded - Requirements are mechanical, not exploratory
- **Brainstorming:** excluded - No ideation phase in packaging

**LLM Features:**
- **Web-Browsing:** excluded - All data is local filesystem
- **File I/O:** included - Core requirement: read workspace files, write setup.md, create zip archive
- **Sub-Agents:** excluded - Single agent (Cog) handles all steps
- **Sub-Processes:** excluded - Linear sequential workflow, no parallelism needed

**Memory:**
- Type: single-session
- Tracking: None (no stepsCompleted in output, no continuation)

**External Integrations:**
- None required

**Installation Requirements:**
- None - all tools are built-in LLM capabilities (file I/O)

---

## Workflow Design

### Step Outline

| Step | File | Type | Goal | Menu |
|------|------|------|------|------|
| 01 | step-01-load-workspace.md | Init (non-continuable) | Get workspace path, validate completeness, extract system name | C only |
| 02 | step-02-metadata-injection.md | Middle (simple) | Inject OCF version and template metadata into workspace artifacts | Auto-proceed |
| 03 | step-03-setup-prompt.md | Middle (standard) | Generate setup.md with installation instructions | C only |
| 04 | step-04-package-assembly.md | Final | Bundle workspace + setup.md into .ocf.zip | None (final) |

### Step Details

**Step 01: Load Workspace**
- Type: Init (non-continuable)
- Goal: Get workspace path from user, validate it contains required artifacts, extract the system name
- Sequence:
  1. Ask user for workspace path
  2. Validate workspace exists at path
  3. Check for required files: SOUL.md, AGENTS.md, USER.md, openclaw.json
  4. Check for optional files: TOOLS.md, MEMORY.md, IDENTITY.md, REVIEW.md, skills/
  5. Extract system name from workspace (from openclaw.json or folder name)
  6. Ask for optional inputs: custom setup instructions, target OCF version
  7. Present validation summary and confirm
- Menu: C only (proceed to metadata injection)
- Output: None (state carried in context)
- Frontmatter refs: nextStepFile

**Step 02: Metadata Injection**
- Type: Middle (simple), auto-proceed
- Goal: Inject OCF version metadata and template origin tracking into workspace artifacts
- Sequence:
  1. Determine OCF version (from module.yaml or user-specified)
  2. Read each workspace artifact that needs metadata
  3. Inject OCF metadata block into AGENTS.md frontmatter (or append section)
  4. Add template-origin tracking comments for upgrade-path support
  5. Confirm injection complete, auto-proceed
- Menu: Auto-proceed (mechanical operation, no user decision needed)
- Output: Modified workspace files (in-place or staging area)
- Frontmatter refs: nextStepFile
- Subprocess: Not needed (small number of files)

**Step 03: Setup Prompt Generation**
- Type: Middle (standard)
- Goal: Generate the companion setup.md document
- Sequence:
  1. Load setup.md template from data/setup-prompt-template.md
  2. Populate template with workspace details:
     - System name and description (from SOUL.md/AGENTS.md)
     - File manifest (list of all workspace files)
     - Prerequisites (OpenClaw installation, required tools)
     - Unpacking instructions (extract zip, place files)
     - Activation procedure (load AGENTS.md, configure memory, etc.)
     - OCF metadata block (version, creation date, template origins)
  3. Include any custom setup instructions from user
  4. Present generated setup.md for review
- Menu: C only (confirm setup.md is acceptable before packaging)
- Output: `{system-name}.setup.md` written to staging area
- Frontmatter refs: nextStepFile, setupPromptTemplate (data file)

**Step 04: Package Assembly**
- Type: Final step
- Goal: Create the .ocf.zip archive and output final paths
- Sequence:
  1. Create `{ocf_output_folder}/packages/` directory if needed
  2. Copy setup.md into workspace directory (or staging)
  3. Create zip archive: `{system-name}.ocf.zip` containing all workspace files + setup.md
  4. Copy setup.md separately to packages/ (for standalone access)
  5. Verify archive contains expected files
  6. Present completion summary with output paths
- Menu: None (final step, workflow complete)
- Output: `{ocf_output_folder}/packages/{system-name}.ocf.zip` and `{ocf_output_folder}/packages/{system-name}.setup.md`
- Frontmatter refs: No nextStepFile (final)

### Data Flow

```
User Input (workspace path, options)
    ↓
Step 01: Validate → workspace_path, system_name, file_manifest
    ↓
Step 02: Inject → modified workspace artifacts with OCF metadata
    ↓
Step 03: Generate → {system-name}.setup.md
    ↓
Step 04: Bundle → {system-name}.ocf.zip + standalone setup.md
```

### File Structure

```
package-export/
├── workflow.md                          # Entry point
├── package-export.spec.md               # Original spec (preserved)
├── data/
│   └── setup-prompt-template.md         # Template for setup.md generation
└── steps-c/
    ├── step-01-load-workspace.md        # Init: validate workspace
    ├── step-02-metadata-injection.md    # Inject OCF metadata
    ├── step-03-setup-prompt.md          # Generate setup.md
    └── step-04-package-assembly.md      # Bundle into .ocf.zip
```

### Role and Persona

- **Agent:** Cog (Gear Wright) -- assembly and packaging specialist
- **Tone:** Technical, precise, methodical
- **Style:** Prescriptive -- exact file operations, not open-ended facilitation
- **Collaboration:** Minimal -- user confirms at checkpoints, agent executes mechanically

### Validation and Error Handling

- Step 01: If workspace path invalid or missing required files → report missing files, halt
- Step 02: If metadata injection fails → report which file failed, halt
- Step 03: If template generation fails → report issue, allow retry
- Step 04: If zip creation fails → report error, suggest manual bundling

### Subprocess Optimization

- Not applicable for this workflow (small number of files, simple operations)
- All operations execute in main thread
- Graceful fallback not needed (no subprocesses designed)

### Special Features

- No branching logic needed
- No workflow chaining (standalone utility)
- No input discovery (user provides workspace path directly)
- web_bundle: true (workflow can be bundled for web distribution)
