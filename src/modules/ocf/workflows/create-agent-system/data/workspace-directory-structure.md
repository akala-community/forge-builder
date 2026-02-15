# OpenClaw Workspace Directory Structure

## Standard Layout

An OpenClaw workspace is a flat directory of Markdown files that configure a single agent. Each file serves a distinct purpose and is loaded by the runtime at the appropriate time.

```
{workspace}/
├── AGENTS.md          # Central operating instructions
├── SOUL.md            # Personality and behavioral principles
├── USER.md            # User profile and context
├── IDENTITY.md        # Agent identity (name, creature, vibe, emoji, avatar)
├── TOOLS.md           # Local tool configuration notes
├── HEARTBEAT.md       # Periodic task checklist (cron-style)
├── MEMORY.md          # Curated long-term memory (free-form)
├── BOOT.md            # Startup instructions (runs every session)
├── BOOTSTRAP.md       # First-run script (deleted after use)
├── memory/            # Daily note logs
│   ├── YYYY-MM-DD.md  # Per-day raw logs
│   └── heartbeat-state.json  # Heartbeat tracking state
└── skills/            # Workspace-scoped skills
    └── {skill-name}/
        ├── SKILL.md
        └── (scripts/, references/, assets/)
```

## Workspace Files

| File | Required | Purpose |
|------|----------|---------|
| `AGENTS.md` | Yes | Core directives, behavioral instructions, and capability definitions |
| `SOUL.md` | No | Personality traits, voice, tone, communication principles |
| `USER.md` | No | User context: preferences, expertise level, working style |
| `IDENTITY.md` | No | Agent identity fields: Name, Creature, Vibe, Emoji, Avatar |
| `TOOLS.md` | No | Notes on locally available tools and environment |
| `HEARTBEAT.md` | No | Periodic tasks the agent should run on a schedule |
| `MEMORY.md` | No | Free-form curated long-term memory written by the agent |
| `BOOT.md` | No | Instructions executed at the start of every session |
| `BOOTSTRAP.md` | No | One-time first-run setup script; deleted after execution |

## Runtime Directories

### memory/

The `memory/` directory holds automatically generated daily logs and heartbeat state.

- `YYYY-MM-DD.md` -- Raw session logs for each day. Created automatically.
- `heartbeat-state.json` -- Tracks heartbeat execution state (last run times, task completion).

### skills/

The `skills/` directory holds workspace-scoped skill definitions. Each skill is a subdirectory containing a `SKILL.md` and optional resource folders.

```
skills/
└── my-skill/
    ├── SKILL.md           # Skill definition (name + description frontmatter, instructions body)
    ├── scripts/           # Executable code (Python, Bash, etc.)
    ├── references/        # Documentation loaded into context
    └── assets/            # Files used in output (templates, images, fonts)
```

## Naming Conventions

- **Workspace files:** UPPER-CASE with `.md` extension (AGENTS.md, SOUL.md, etc.)
- **Skill folders:** kebab-case matching the skill name (e.g., `my-skill/`)
- **Skill definition:** Always `SKILL.md` inside the skill folder
- **Resource directories:** Lowercase (`scripts/`, `references/`, `assets/`)

## openclaw.json Configuration

The `openclaw.json` file is the runtime configuration for OpenClaw. It is NOT stored inside the workspace directory. Its location depends on the platform:

| Platform | Location |
|----------|----------|
| macOS | `~/Library/Application Support/openclaw/openclaw.json` |
| Linux | `~/.config/openclaw/openclaw.json` |
| Windows | `%APPDATA%\openclaw\openclaw.json` |

The `openclaw.json` file configures:

- **Workspace path:** Where the workspace directory is located
- **Model settings:** Which LLM model and provider to use
- **Skill paths:** Additional directories to search for skills (beyond the workspace `skills/` folder)
- **Gateway settings:** API gateway configuration if applicable
- **Feature flags:** Runtime feature toggles

The workspace directory itself is self-contained. All agent behavior is defined by the Markdown files within it. The `openclaw.json` file connects the runtime to the workspace and configures operational parameters that live outside the agent's persona.
