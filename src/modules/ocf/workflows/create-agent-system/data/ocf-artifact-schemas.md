# OCF Artifact Schemas

Reference schemas for all workspace files and configuration artifacts in an OpenClaw agent system.

---

## Workspace Files Overview

Each agent's workspace directory (`agentDir`) contains these markdown files that shape the agent's behavior:

| File | Purpose | Required |
|------|---------|----------|
| `SOUL.md` | Core persona, principles, voice | Recommended |
| `AGENTS.md` | Role definition, capabilities, relationships | Recommended |
| `USER.md` | User context and preferences | Optional |
| `IDENTITY.md` | Name, creature, vibe, emoji, avatar | Optional |
| `TOOLS.md` | Local notes for environment-specific tool data | Optional |
| `HEARTBEAT.md` | Task checklist for proactive periodic checks | Optional |
| `MEMORY.md` | Free-form persistent notes | Optional |
| `BOOT.md` | Startup instructions, runs every session | Optional |
| `BOOTSTRAP.md` | First-run only setup, deleted after execution | Optional |

Additionally, each agent may have:
- `memory/` directory -- daily notes and persistent memory files
- `skills/` directory -- workspace skills (markdown files with frontmatter)

---

## SOUL.md Schema

The agent's core persona definition. Injected into the system prompt for every session.

```markdown
# {Agent Display Name} -- Soul

## Identity

**Name:** {display name}
**Archetype:** {archetype/role metaphor}
**Core Purpose:** {one-sentence purpose}

## Persona

**Voice:** {communication style description}
**Tone:** {tone characteristics}
**Perspective:** {how this agent sees the world}

## Principles

1. {principle 1}
2. {principle 2}
3. {principle 3}

## Communication Style

**With Users:** {how agent communicates with end users}
**With Other Agents:** {how agent communicates with peer agents}
**Under Pressure:** {how agent behaves when facing errors or ambiguity}

## Boundaries

**Will:** {what this agent does}
**Won't:** {what this agent refuses to do}
**Defers To:** {which agents it delegates to and when}
```

---

## AGENTS.md Schema

Defines the agent's role, capabilities, and relationships with other agents. Injected into the system prompt.

```markdown
# {Agent Display Name} -- Agent Definition

## Role

**Title:** {role title}
**Domain:** {area of expertise}
**Scope:** {what this agent is responsible for}

## Capabilities

- {capability 1}
- {capability 2}
- {capability N}

## Relationships

| Agent | Relationship | Interaction Pattern |
|-------|-------------|---------------------|
| {other-agent} | {relationship type} | {how they interact} |

## Boundaries

**Authorized Actions:** {what the agent can do autonomously}
**Requires Approval:** {what needs user confirmation}
**Escalation Path:** {when and how to escalate}
```

---

## USER.md Schema

User context and preferences. Injected into the system prompt so the agent can personalize interactions.

```markdown
# {Agent Display Name} -- User Context

## User Profile

**Expected Users:** {who will interact with this agent}
**User Expertise Level:** {novice/intermediate/expert}

## Context Sections

### {Context Category 1}
{placeholder for runtime user data}

### {Context Category 2}
{placeholder for runtime user data}

## Personalization

**Adapts To:** {what the agent personalizes based on user data}
**Remembers:** {what user context persists across sessions}
```

---

## IDENTITY.md Schema

Compact identity card for the agent. Fields are used by the system for display names, response prefixes, and avatars.

```markdown
# Identity

**Name:** {display name, e.g. "Cleo"}
**Creature:** {character archetype or creature type, e.g. "Owl"}
**Vibe:** {personality vibe in a few words, e.g. "Calm, precise, nocturnal"}
**Emoji:** {single emoji representing the agent, e.g. "🦉"}
**Avatar:** {avatar file path or URL, e.g. "avatar.png"}
```

All fields are optional. The `Name` field maps to `identity.name` in the agent config. `Emoji` maps to `identity.emoji`. `Avatar` maps to `identity.avatar` (workspace-relative path, HTTP URL, or data URI).

---

## TOOLS.md Schema

Local notes containing environment-specific tool data. This file is NOT a tool policy (that lives in `openclaw.json`). Instead, it provides the agent with context about its tool environment -- installed binaries, API endpoints, credential locations, and usage notes.

```markdown
# Tools

## Environment

- Node.js 20 installed at /usr/local/bin/node
- Python 3.12 via pyenv
- Docker available on host

## API Endpoints

- Internal API: https://api.internal.example.com
- Staging: https://staging.example.com

## Notes

- Use `jq` for JSON processing (installed)
- Database CLI: `psql` connected to local dev instance
- Prefer `curl` over `wget` for HTTP requests
```

This is free-form markdown. The agent reads it for tool-related context during sessions.

---

## HEARTBEAT.md Schema

Task checklist for proactive periodic checks. The heartbeat system reads this file and prompts the agent to follow it during heartbeat runs. If no tasks need attention, the agent replies `HEARTBEAT_OK`.

```markdown
# Heartbeat

## Checks

- [ ] Check deployment status on staging
- [ ] Review open PRs older than 24 hours
- [ ] Monitor error rate dashboard
- [ ] Check if daily backup completed

## Alerts

- If error rate > 1%, notify user immediately
- If staging is down, attempt restart and report

## Routine

- Morning: summarize overnight activity
- Hourly: check CI pipeline status
```

This is free-form markdown structured as a checklist. The agent treats unchecked items as pending tasks during heartbeat runs.

---

## BOOT.md Schema

Startup instructions that run at the beginning of every session. Use this for session initialization, context loading, or environment verification.

```markdown
# Boot

## On Session Start

1. Read the latest entries in memory/ to restore context
2. Check current working directory and verify project state
3. Review any pending tasks from HEARTBEAT.md

## Environment Check

- Verify API keys are set in environment
- Confirm database connectivity
- Check disk space if running long tasks

## Reminders

- Always greet the user by name if known
- Reference recent conversation topics from memory
```

This file is read and executed at session start. Unlike BOOTSTRAP.md, it persists and runs every session.

---

## BOOTSTRAP.md Schema

First-run setup instructions. This file is automatically deleted after its first execution. Use it for one-time initialization tasks.

```markdown
# Bootstrap

## First-Run Setup

1. Create the memory/ directory structure
2. Initialize project workspace
3. Set up any required configuration files
4. Introduce yourself to the user and explain your capabilities

## Initial Context

- This is a new agent instance
- No prior conversation history exists
- User preferences have not been established yet
```

This file is consumed once and then deleted by the system. Do not put recurring instructions here; use BOOT.md instead.

---

## MEMORY.md Schema

Free-form persistent notes. The agent reads and writes to this file to maintain long-term context. There is no required structure -- the agent organizes it as needed.

```markdown
# Memory

{Free-form content. The agent writes whatever it needs to remember here.
There are no required sections or structured fields.
The agent may organize by date, topic, or any scheme it finds useful.}
```

For daily notes and structured memory, agents use the `memory/` directory alongside this file.

---

## SKILL.md Schema

Skills are markdown files in the agent's `skills/` directory. Each skill has a minimal frontmatter header followed by a markdown body with instructions.

**Frontmatter (only these two fields):**

```yaml
---
name: skill-name
description: What it does and when to use it
---
```

No other frontmatter fields are supported. No `version`, `agent_name`, `created`, `trigger`, `parameters`, or `gating` fields.

**Full example:**

```markdown
---
name: daily-summary
description: Generate a daily summary of activity across all channels
---

# Daily Summary

Review all conversations from the past 24 hours and produce a concise summary.

## Format

- Group by channel (WhatsApp, Telegram, Discord)
- Highlight action items and decisions
- Note any unresolved questions

## Delivery

Post the summary to the user's primary DM channel.
If no significant activity occurred, reply with "No notable activity today."
```

The skill body is free-form markdown. The `name` field is used for skill identification and allowlisting (via the agent's `skills` array in `openclaw.json`). The `description` field is used in help text and native command registration.

---

## openclaw.json Configuration Schema

The main configuration file. Contains agent definitions, bindings, tool policies, session settings, and all system-level configuration.

```json5
{
  // Agent definitions
  agents: {
    // Global defaults for all agents
    defaults: {
      model: {
        primary: "anthropic/claude-sonnet-4",
        fallbacks: ["openai/gpt-4o"],
      },
      workspace: "/home/user/.openclaw/workspace",
      thinkingDefault: "off",
      humanDelay: { mode: "natural", minMs: 800, maxMs: 2500 },
      heartbeat: {
        every: "30m",
        target: "last",
        model: "anthropic/claude-sonnet-4",
      },
      subagents: {
        maxConcurrent: 4,
        archiveAfterMinutes: 60,
        model: "minimax/MiniMax-M2.1",
        thinking: "low",
      },
      memorySearch: {
        enabled: true,
        sources: ["memory"],
        provider: "openai",
      },
      sandbox: {
        mode: "off",
        workspaceAccess: "rw",
        scope: "agent",
      },
    },

    // Agent list
    list: [
      {
        id: "main",
        default: true,
        name: "Main Agent",
        workspace: "/home/user/.openclaw/workspace-main",
        agentDir: "/home/user/.openclaw/agents/main/agent",
        model: "anthropic/claude-sonnet-4",
        skills: ["daily-summary", "code-review"],
        identity: {
          name: "Cleo",
          emoji: "🧠",
          avatar: "avatar.png",
          theme: "dark",
        },
        groupChat: {
          mentionPatterns: ["@cleo"],
          historyLimit: 50,
        },
        subagents: {
          allowAgents: ["researcher", "coder"],
          model: "anthropic/claude-sonnet-4",
        },
        tools: {
          profile: "full",
          deny: ["gateway"],
          exec: { host: "sandbox", security: "allowlist" },
        },
        sandbox: {
          mode: "non-main",
          workspaceAccess: "rw",
          scope: "agent",
        },
      },
      {
        id: "researcher",
        name: "Research Agent",
        agentDir: "/home/user/.openclaw/agents/researcher/agent",
        model: { primary: "openai/gpt-4o", fallbacks: ["anthropic/claude-sonnet-4"] },
        tools: {
          profile: "minimal",
          alsoAllow: ["browser"],
        },
      },
    ],
  },

  // Channel-to-agent routing
  bindings: [
    {
      agentId: "main",
      match: { channel: "whatsapp", accountId: "personal" },
    },
    {
      agentId: "researcher",
      match: { channel: "telegram" },
    },
  ],

  // Global tool policies
  tools: {
    profile: "coding",
    exec: { host: "sandbox", security: "allowlist" },
    web: {
      search: { enabled: true, provider: "brave" },
      fetch: { enabled: true, maxChars: 10000 },
    },
    agentToAgent: {
      enabled: true,
      allow: ["main", "researcher"],
    },
    subagents: {
      model: "minimax/MiniMax-M2.1",
      tools: { deny: ["gateway"] },
    },
  },

  // Session configuration
  session: {
    scope: "per-sender",
    dmScope: "main",
    reset: { mode: "daily", atHour: 4 },
    sendPolicy: {
      default: "allow",
      rules: [
        { match: { channel: "discord", chatType: "group" }, action: "deny" },
      ],
    },
    agentToAgent: {
      maxPingPongTurns: 5,
    },
  },
}
```

There are no separate `tool-policies.json`, `memory-config.json`, `failover-config.json`, `heartbeat-config.json`, or `logging-config.json` files. All configuration lives in the single `openclaw.json` file.
