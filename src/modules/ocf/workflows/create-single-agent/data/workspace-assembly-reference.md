# Workspace Assembly Reference

## Workspace Directory Structure

```
{agent-name}/
├── IDENTITY.md
├── SOUL.md
├── AGENTS.md
├── USER.md
├── MEMORY.md
├── TOOLS.md
├── BOOTSTRAP.md
├── HEARTBEAT.md
├── memory/
├── skills/
│   ├── {skill-1}/
│   │   └── SKILL.md
│   ├── {skill-2}/
│   │   └── SKILL.md
│   └── ...
└── config/
    └── openclaw-fragment.json
```

## Workspace Summary Template

Present after all files are written:

"**Your agent workspace is assembled!**

---

**{agent-name}** — {agent-title}

**Workspace:** `{ocfOutputFolder}/{agent-name}/`

**Files Created:**

| File | Purpose | Status |
|------|---------|--------|
| IDENTITY.md | Agent name, creature type, vibe, emoji | Created |
| SOUL.md | Agent persona, core truths, boundaries | Created |
| AGENTS.md | Workspace operational rules and conventions | Created |
| USER.md | Human context and profile | Created |
| MEMORY.md | Long-term curated memories | Created |
| TOOLS.md | Local tool and environment notes | Created |
| BOOTSTRAP.md | First-run conversation ritual | Created |
| HEARTBEAT.md | Periodic check task list | Created |
| skills/{skill-1}/SKILL.md | {skill-1 description} | Created |
| skills/{skill-2}/SKILL.md | {skill-2 description} | Created |
| config/openclaw-fragment.json | OpenClaw configuration fragment | Created |
| memory/ | Daily memory log directory | Created |

---

**Quick Stats:**
- **Skills:** {count}
- **Channels:** {channel list}
- **Memory:** {session/persistent/both}

---"

## Completion Message Template

"**Your agent has been forged!**

---

**{agent-name}** — {agent-title} {icon}

**Workspace:** `{ocfOutputFolder}/{agent-name}/`

---

**What's Next:**

1. **Test your agent** — Load the workspace in OpenClaw and run a test conversation
2. **Production hardening** — Use OCF's `configure-production-hardening` workflow to add failover, logging, and advanced memory config
3. **Integrate** — Merge `config/openclaw-fragment.json` into your main `openclaw.json`
4. **Iterate** — Use OCF's `edit-agent-system` workflow to evolve your agent's persona and capabilities over time

**To deploy:**
- Copy the workspace folder to your OpenClaw agents directory
- Merge the config fragment into openclaw.json
- Restart your OpenClaw instance

---

**Thank you for forging with me, {user_name}. Every agent deserves a soul worth remembering — and yours has one.**"
