# Review & Completion Templates

Templates used by step-08-review for workspace overview and final completion summary.

---

## Workspace Overview Template

Present this when starting the review:

```markdown
**Workspace Review: {System Display Name}**

**System Name:** {system_name}
**Workspace Location:** {ocf_output_folder}/{system_name}/
**Agent Count:** {number of agents}
**Total Files:** {total file count from manifest}

---

**Agents:**

| # | Agent | Artifacts | Skills |
|---|-------|-----------|--------|
| 1 | {agent-1-display-name} ({agent-1-name}) | SOUL, AGENTS, USER, MEMORY, REVIEW | {skill count} skills |
| 2 | {agent-2-display-name} ({agent-2-name}) | SOUL, AGENTS, USER, MEMORY, REVIEW | {skill count} skills |
...

**System Configuration:**

| Config File | Status |
|-------------|--------|
| openclaw.json | Assembled |
| tool-policies.json | Written |
| memory-config.json | Written |
| failover-config.json | Written |
| heartbeat-config.json | Written |
| logging-config.json | Written |

---

**Your workspace is assembled and ready for review.**
**Would you like to review specific agents, edit artifacts, or mark the workspace as complete?**
```

---

## Final Summary Template

Present this when the user confirms completion:

```markdown
**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**

# Workspace Complete: {System Display Name}

**System:** {system_name}
**Workspace Location:** {ocf_output_folder}/{system_name}/
**Completed:** {current_date}

---

## What Was Built

**Agents:** {agent count}

| Agent | Role | Artifacts | Skills |
|-------|------|-----------|--------|
| {agent-1} | {role} | 5 core files | {skill count} |
| {agent-2} | {role} | 5 core files | {skill count} |
...

**System Configuration:** 6 config files

**Total Files:** {total count}

---

## Workspace Structure

{system_name}/
├── agents/
│   ├── {agent-1}/
│   │   ├── SOUL.md
│   │   ├── AGENTS.md
│   │   ├── USER.md
│   │   ├── MEMORY.md
│   │   ├── REVIEW.md
│   │   └── skills/
│   │       └── {skills...}
│   └── ...
└── config/
    ├── openclaw.json
    ├── tool-policies.json
    ├── memory-config.json
    ├── failover-config.json
    ├── heartbeat-config.json
    └── logging-config.json

---

## Next Steps

- **Test your agents:** Load individual agents and verify their behavior matches your vision
- **Integrate:** Connect the workspace to your OpenClaw environment
- **Iterate:** Use the individual artifact files to refine agent behavior over time
- **Monitor:** Use the config files (heartbeat, logging, failover) to observe system health

**Your agent system workspace is ready to use.**

**━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━**
```
