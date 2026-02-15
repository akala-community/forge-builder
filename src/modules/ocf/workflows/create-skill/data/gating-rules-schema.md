# Skill Frontmatter and Dependency Handling

This document describes the real SKILL.md frontmatter format and how dependencies are managed in OpenClaw skills.

## SKILL.md Frontmatter

OpenClaw skills use minimal YAML frontmatter. The only required fields are `name` and `description`.

### Required Fields

| Field | Type | Description |
|-------|------|-------------|
| `name` | `string` | Skill name in kebab-case (lowercase letters, digits, hyphens). Max 64 characters. |
| `description` | `string` | What the skill does and when to use it. Max 1024 characters. No angle brackets. |

### Optional Fields

| Field | Type | Description |
|-------|------|-------------|
| `license` | `string` | License identifier for the skill |
| `allowed-tools` | varies | Tool access declarations |
| `metadata` | `object` | Additional metadata (see below) |

### Minimal Example

```yaml
---
name: my-skill
description: "Description of what this skill does. Use when the user asks to..."
---
```

### With Optional Metadata

The `metadata` field can contain an `openclaw` object with optional hints for the runtime:

```yaml
---
name: weather
description: Get current weather and forecasts (no API key required).
metadata: { "openclaw": { "emoji": "icon" } }
---
```

## The Description as Trigger Mechanism

The `description` field is the primary mechanism by which the runtime decides when to load a skill. It should clearly state:

1. **What** the skill does
2. **When** to use it -- specific scenarios, file types, tasks, or user requests that should activate it

Good descriptions are specific and action-oriented:

```yaml
description: "Interact with GitHub using the `gh` CLI. Use `gh issue`, `gh pr`, `gh run`, and `gh api` for issues, PRs, CI runs, and advanced queries."
```

```yaml
description: Get current weather and forecasts (no API key required).
```

The runtime uses progressive disclosure: it reads the description first, and only loads the full SKILL.md body (and bundled resources) when the skill is relevant to the current task.

## Dependency Handling

OpenClaw skills do NOT use gating rules or requirement blocks in frontmatter to enforce dependencies. Instead, dependencies are handled through the skill body and optional scripts.

### Approach 1: Instructions in the Skill Body

The most common approach. The SKILL.md body tells the agent what tools are needed and how to install them. The agent follows these instructions like any other task.

```markdown
## Prerequisites

This skill requires the `gh` CLI. Install it with:

- macOS: `brew install gh`
- Linux: See https://github.com/cli/cli/blob/trunk/docs/install_linux.md
- Windows: `winget install GitHub.cli`

After installing, authenticate with `gh auth login`.
```

### Approach 2: Setup Scripts

For skills with complex installation requirements, a setup script in the `scripts/` directory can automate dependency installation:

```
my-skill/
├── SKILL.md
└── scripts/
    └── setup.sh    # Installs dependencies
```

The SKILL.md body references the script:

```markdown
## Setup

Run the setup script to install all dependencies:

```bash
bash scripts/setup.sh
```
```

### Approach 3: Runtime Metadata Hints

Some published skills include dependency hints in the `metadata.openclaw` block. These are informational hints that the runtime can use to check prerequisites or suggest installation steps, but they do not gate or block skill usage:

```yaml
metadata:
  openclaw:
    requires: { "bins": ["gh"] }
    install:
      - { "kind": "brew", "formula": "gh", "bins": ["gh"] }
```

These hints are optional and supplementary to the instructions in the skill body.

## Scaffolding and Validation Tools

### init_skill.py

Located at `skills/skill-creator/scripts/init_skill.py`. Creates a new skill directory from a template.

```bash
python init_skill.py my-skill --path skills/
python init_skill.py my-skill --path skills/ --resources scripts,references
python init_skill.py my-skill --path skills/ --resources scripts --examples
```

The generated SKILL.md includes only `name` and `description` in the frontmatter, with TODO placeholders in the body.

### package_skill.py

Located at `skills/skill-creator/scripts/package_skill.py`. Validates and packages a skill into a distributable `.skill` file (zip format).

```bash
python package_skill.py path/to/my-skill
python package_skill.py path/to/my-skill ./dist
```

Validation checks performed (via `quick_validate.py`):

- SKILL.md exists in the skill directory
- Valid YAML frontmatter is present
- Only allowed frontmatter keys are used (`name`, `description`, `license`, `allowed-tools`, `metadata`)
- `name` is present and in valid kebab-case format (max 64 characters)
- `description` is present and within length/format constraints (max 1024 characters, no angle brackets)
- Name does not start/end with hyphens or contain consecutive hyphens

## Skill Directory Structure

```
{skill-name}/
├── SKILL.md           # Required. Frontmatter + instructions.
├── scripts/           # Optional. Executable code (Python, Bash, etc.)
├── references/        # Optional. Documentation loaded into context.
└── assets/            # Optional. Files used in output (templates, images, fonts).
```

Not every skill needs resource directories. Many skills consist of only a SKILL.md file.
