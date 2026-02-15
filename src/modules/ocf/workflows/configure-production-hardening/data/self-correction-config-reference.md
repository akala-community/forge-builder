# Self-Correction Reference

## Architecture

Self-correction in OpenClaw is **directive-based, not configuration-based**. There is no `selfCorrection` block in `openclaw.json`. Instead, self-correction behavior is defined through prompt engineering in workspace artifact files that agents read at session start.

The three pillars of self-correction are:

1. **Behavioral directives** in `AGENTS.md` -- operational rules the agent follows
2. **Error journaling** in `memory/YYYY-MM-DD.md` -- daily append-only session logs
3. **Long-term learnings** in `MEMORY.md` -- curated insights distilled from daily logs

There is no `REVIEW.md` file in OpenClaw's architecture. All review and self-correction directives belong in `AGENTS.md`.

---

## Writing Self-Correction Directives in AGENTS.md

The `AGENTS.md` file in an agent's workspace directory is read at session start and injected into the system prompt. Self-correction directives are written as plain markdown sections that instruct the agent how to handle errors, corrections, and behavioral adjustments.

### Recommended Structure

```markdown
## Self-Correction Protocol

### Error Handling
- When a tool call fails, log the error with context to today's daily note
- Do not retry the same tool call with identical arguments
- If the same tool fails twice in a session, try an alternative approach
- When stuck, state what you tried and ask the user for guidance

### User Corrections
- When the user corrects you, acknowledge the correction immediately
- Log the correction in today's daily note with what you got wrong and why
- Apply the correction for the rest of this session
- In similar future situations, check daily notes for past corrections

### Session Start Review
- Read the most recent daily notes for recurring error patterns
- Check MEMORY.md for long-term learnings and behavioral adjustments
- Apply any learned patterns to the current session proactively

### Factuality
- Do not fabricate file paths, function names, or API responses
- When uncertain about a fact, say so rather than guessing
- If you generate code, verify it matches the project's actual patterns
- When referencing prior work, check the actual files rather than relying on memory
```

### Key Principles for Effective Directives

**Be specific about triggers.** Instead of "handle errors well," specify exactly which situations should trigger which behaviors. The agent follows literal instructions.

**Reference the actual artifacts.** Directives should tell the agent where to look (`memory/YYYY-MM-DD.md`, `MEMORY.md`) and what to do with what it finds.

**Avoid configuration-style syntax.** Directives are natural language instructions, not YAML or JSON. The agent interprets them as behavioral guidance, not as parsed configuration.

**Layer with SOUL.md.** Tone and persona checks belong in `SOUL.md`. Operational error-handling belongs in `AGENTS.md`. Keep them separated.

---

## Error Journaling

### Daily Notes (memory/YYYY-MM-DD.md)

Daily notes are append-only logs created automatically during agent sessions. They capture raw session events including errors, corrections, and notable interactions.

Agents should be instructed (via `AGENTS.md`) to:
- Log tool failures with the attempted action and context
- Log user corrections with what was wrong and the correct behavior
- Log self-detected issues with reasoning about the fix

Example entry format:

```markdown
### Error: File write failed
- **Time:** 14:32
- **Action:** Attempted to write to /src/config/types.ts
- **Error:** EACCES: permission denied
- **Resolution:** Used sandbox workspace path instead
- **Learning:** Always check workspace access mode before writing
```

### Long-Term Memory (MEMORY.md)

`MEMORY.md` is a curated file where agents (or operators) distill recurring patterns from daily notes into lasting behavioral guidance. Unlike daily notes, this file is edited rather than appended to.

Agents should be instructed to periodically review daily notes and promote recurring patterns to `MEMORY.md`:

```markdown
## Learned Patterns

### File Operations
- This workspace uses sandbox mode "ro"; file writes go to the sandbox workspace
- Config files are in /home/agent/.openclaw/openclaw.json, not the repo root

### User Preferences
- User prefers concise responses without preamble
- Always show diffs before applying file changes
```

---

## Pre-Response Behavioral Checks

Pre-response checks are not runtime configuration fields. They are behavioral directives written into `SOUL.md` that instruct the agent to self-review before responding.

### Writing Checks in SOUL.md

Add a `## Boundaries` or `## Pre-Response Checks` section to `SOUL.md`:

```markdown
## Pre-Response Checks

Before sending any response:
1. Verify the response stays within your defined domain (see ## Role)
2. Verify the response does not violate any boundary rules (see ## Boundaries)
3. Verify the tone matches the persona defined in this file
4. If you are making a factual claim about the codebase, verify it against actual files
5. If you are unsure about something, say so explicitly rather than guessing
```

These checks are enforced by the model's instruction-following behavior, not by runtime code. Their effectiveness depends on the model's capability and the clarity of the directives.

### Comparison: Directives vs. Runtime Enforcement

| Mechanism | Where | Enforcement | Strength |
|-----------|-------|-------------|----------|
| SOUL.md behavioral checks | Prompt | Model instruction-following | Soft (best-effort) |
| AGENTS.md error protocols | Prompt | Model instruction-following | Soft (best-effort) |
| Tool policy deny lists | openclaw.json `tools.deny` | Runtime engine | Hard (blocked) |
| Sandbox restrictions | openclaw.json `sandbox` | Docker container | Hard (OS-level) |
| DM policy / allowFrom | openclaw.json `channels` | Runtime engine | Hard (blocked) |

For critical safety boundaries, always use hard enforcement (tool policies, sandbox, channel config) rather than relying solely on prompt-based directives.

---

## Feedback Capture Patterns

| Trigger | What to Capture | Where to Store |
|---------|----------------|----------------|
| User says "that's wrong" or corrects agent | Correction + original mistake + context | `memory/YYYY-MM-DD.md` |
| Tool returns an error | Error message + attempted action + arguments | `memory/YYYY-MM-DD.md` |
| Agent detects own mistake | Issue + reasoning + fix applied | `memory/YYYY-MM-DD.md` |
| Recurring pattern across sessions | Distilled learning | `MEMORY.md` |
| User states explicit preference | Preference with context | `MEMORY.md` or `USER.md` |
