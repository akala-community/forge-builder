# Assembly Templates

Templates used by step-07-assembly for file manifest and assembly summary output.

---

## File Manifest Template

Append this section to workspace-plan.md after all files are written:

```markdown
## File Manifest

**Assembly Date:** {current_date}
**Total Files Written:** {count}
**Total Directories Created:** {count}

### Agent Artifacts

| Agent | File | Path | Status |
|-------|------|------|--------|
| {agent-1} | SOUL.md | {full path} | Written |
| {agent-1} | AGENTS.md | {full path} | Written |
| {agent-1} | USER.md | {full path} | Written |
| {agent-1} | MEMORY.md | {full path} | Written |
| {agent-1} | REVIEW.md | {full path} | Written |
| {agent-1} | skills/{skill}.md | {full path} | Written |
...

### System Config

| File | Path | Status |
|------|------|--------|
| openclaw.json | {full path} | Written |
| tool-policies.json | {full path} | Written |
| memory-config.json | {full path} | Written |
| failover-config.json | {full path} | Written |
| heartbeat-config.json | {full path} | Written |
| logging-config.json | {full path} | Written |
```

---

## Assembly Summary Template

Present this after assembly completes:

```markdown
**Assembly complete.**

**System:** {system_name}
**Workspace Location:** {ocf_output_folder}/{system_name}/

**Directory Tree:**

{system_name}/
├── agents/
│   ├── {agent-1}/
│   │   ├── SOUL.md
│   │   ├── AGENTS.md
│   │   ├── USER.md
│   │   ├── MEMORY.md
│   │   ├── REVIEW.md
│   │   └── skills/
│   │       ├── {skill-1}.md
│   │       └── {skill-2}.md
│   ├── {agent-2}/
│   │   └── ...
│   └── ...
└── config/
    ├── openclaw.json
    ├── tool-policies.json
    ├── memory-config.json
    ├── failover-config.json
    ├── heartbeat-config.json
    └── logging-config.json

**Files Written:** {total file count}
**Directories Created:** {total directory count}
**Agents Assembled:** {agent count}
**Skills Assembled:** {total skill count across all agents}
**Config Files:** 6

**All artifacts have been extracted from workspace-plan.md and written to individual files.**

**Next:** Review — interactive review and refinement of the complete workspace.
```
