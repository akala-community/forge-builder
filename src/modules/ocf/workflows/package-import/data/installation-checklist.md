# Installation Checklist

Reference data for the package-import workflow. These rules define what constitutes a valid OCF package import.

---

## Package Validation

| Check | Severity | Rule |
|-------|----------|------|
| Archive exists | FAIL | .ocf.zip file must exist at the provided path. |
| Archive is valid zip | FAIL | File must be a valid zip archive that can be extracted. |
| Setup prompt exists | FAIL | setup.md file must exist at the provided path. |
| Setup prompt is non-empty | FAIL | setup.md must contain installation instructions. |

## Extraction Checks

| Check | Severity | Rule |
|-------|----------|------|
| Target directory accessible | FAIL | Target workspace directory must exist or be creatable. |
| No existing workspace conflict | WARN | If target already contains workspace files, warn before overwrite. |
| Required workspace files present | FAIL | Archive must contain at minimum SOUL.md and AGENTS.md. |
| Directory structure valid | WARN | Archive should follow standard workspace structure (memory/, skills/, etc.). |

## Configuration Merge Checks

| Check | Severity | Rule |
|-------|----------|------|
| openclaw.json exists at target | WARN | If no existing openclaw.json, package config will be installed fresh. |
| No agent name conflicts | WARN | New agent entries should not conflict with existing agent names. |
| Binding channels valid | WARN | Binding channel references should be valid or flagged for review. |
| Model references valid | WARN | Model configuration references should be valid provider/model pairs. |

## Registration Checks

| Check | Severity | Rule |
|-------|----------|------|
| Agent entry complete | FAIL | Each agent must have workspace path, name, and model configuration. |
| Workspace path resolves | FAIL | Registered workspace path must point to existing directory with SOUL.md. |
| Binding targets valid | WARN | Each binding should have a valid channel and target (accountId or peer). |

## Activation Checks

| Check | Severity | Rule |
|-------|----------|------|
| SOUL.md readable | FAIL | Agent's SOUL.md must be readable and non-empty. |
| AGENTS.md readable | FAIL | Agent's AGENTS.md must be readable and non-empty. |
| Configuration consistent | WARN | Merged openclaw.json should pass basic consistency checks. |
