# Workflow Specification: package-forge

**Module:** forge
**Status:** Placeholder — To be created via create-workflow workflow
**Created:** 2026-02-13

---

## Workflow Overview

**Goal:** Bundle The Forge into an installable .ocf.zip package for distribution

**Description:** Collects all generated workspace files, skills, reference data, and configuration into a single .ocf.zip archive that can be installed into any OpenClaw instance. Injects metadata and generates a setup prompt for first-run configuration.

**Workflow Type:** Build / Packaging

---

## Workflow Structure

### Entry Point

```yaml
---
name: package-forge
description: Bundle The Forge into installable .ocf.zip
web_bundle: true
installed_path: '{project-root}/_bmad/forge/workflows/package-forge'
---
```

### Mode

- [x] Create-only (steps-c/)
- [ ] Tri-modal (steps-c/, steps-e/, steps-v/)

---

## Planned Steps

| Step | Name | Goal |
|------|------|------|
| 01 | Validate pre-package | Run validate-forge to ensure consistency before packaging |
| 02 | Collect artifacts | Gather all workspace files, skills, and reference data |
| 03 | Inject metadata | Add version, build date, compatibility info |
| 04 | Generate setup prompt | Create first-run setup instructions for the installer |
| 05 | Bundle .ocf.zip | Create the archive |
| 06 | Verify package | Test the archive can be extracted and passes basic checks |

---

## Workflow Inputs

### Required Inputs

- All generated workspace files (SOUL.md, AGENTS.md, IDENTITY.md)
- All generated skill files
- Reference data (patterns library, config reference)
- Version number

### Optional Inputs

- Release notes
- Changelog

---

## Workflow Outputs

### Output Format

- [ ] Document-producing
- [x] Non-document

### Output Files

- `{forge_artifacts}/forge-{version}.ocf.zip` — Installable package
- `{forge_artifacts}/RELEASE.md` — Release notes (if provided)

---

## Agent Integration

### Primary Agent

Forge Builder (Morgan)

### Other Agents

None

---

## Implementation Notes

**Use the create-workflow workflow to build this workflow.**

Inputs needed:
- Workflow name and description
- Step structure and sequence
- Input/output specifications
- Agent associations
- .ocf.zip format specification

---

_Spec created on 2026-02-13 via BMAD Module workflow_
