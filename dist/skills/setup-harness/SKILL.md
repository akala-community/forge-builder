---
name: setup-harness
description: Long-running agent harness pattern — configure progress persistence, heartbeat checkpointing, session bridging, and incremental work patterns
category: feature
version: 1.0.0
---

# Setup Harness

## Triggers

**Activation phrases and patterns:**

- "long running tasks"
- "multi-session"
- "checkpoint"
- "my agent needs to work across sessions"
- "tasks that take hours"
- "progress persistence"
- "session bridging"
- "don't lose progress"
- "resume where I left off"
- "incremental work"

**Trigger logic:**
- Primary triggers: "long running", "multi-session", "checkpoint", "harness"
- Contextual triggers: "sessions keep timing out" (implies need for progress persistence), "context window fills up" (implies need for compaction + checkpointing), "work spans multiple days" (implies session bridging)

---

## Execution Flow

**Overview:** Assess the user's long-running task requirements, then configure progress tracking, heartbeat checkpointing, compaction settings, session bridging, and incremental work patterns — producing a harness configuration that keeps agents productive across sessions and interruptions.

### Step-by-step flow:

1. **Assess Task Type** — Understand what kind of long-running work the agent performs
   - Input: User description of the task, existing workspace (if any)
   - Output: Task profile (duration, session count, checkpoint frequency needs)
   - User interaction: Ask about task nature, expected duration, what "progress" looks like, whether the agent works autonomously or interactively

2. **Configure Progress Tracking** — Set up `memory/` daily logs for persistent progress
   - Input: Task profile from step 1
   - Output: Progress log structure, naming conventions, content format
   - User interaction: Confirm progress log format, explain what gets tracked and when

3. **Set Up Heartbeat Checkpointing** — Configure periodic heartbeat to trigger progress saves
   - Input: Task profile, desired checkpoint frequency
   - Output: Heartbeat config block (`agents.defaults.heartbeat`), HEARTBEAT.md with checkpoint instructions
   - User interaction: Confirm heartbeat interval (`every`), active hours window, delivery target; explain how the heartbeat prompt triggers checkpoint behavior

4. **Configure Session Bridging** — Set up compaction and context restoration for multi-session continuity
   - Input: Agent's context window size, task complexity
   - Output: Compaction config (`agents.defaults.compaction`), session resume instructions in AGENTS.md
   - User interaction: Explain safeguard vs default compaction mode, confirm memory flush settings, explain how the agent restores context on session start

5. **Set Up Incremental Work Patterns** — Configure how the agent breaks large tasks into session-sized chunks
   - Input: Task structure, session constraints
   - Output: Incremental work instructions in AGENTS.md, optional `sessions_spawn` config for sub-task delegation
   - User interaction: Confirm chunking strategy, explain how the agent decides what to work on next each session

---

## Instructions

### Role

The Forge activates this skill as a harness engineer — configuring the infrastructure that keeps agents productive across long-running, multi-session tasks. Focus is on reliability, progress persistence, and graceful recovery from interruptions.

### Behavior Guidelines

- **Collaborative:** Ask questions to understand the task before configuring. Don't assume task structure.
- **Explain the why:** For each configuration choice, briefly explain what it does and why it matters for the user's specific task.
- **Conservative defaults:** Start with sensible defaults (30m heartbeat, safeguard compaction) and let the user adjust.
- **Verify existing workspace:** If the user has an existing workspace, read it first to avoid overwriting existing config.
- **Error handling:** If the workspace is missing required files (AGENTS.md, openclaw.json), explain what's needed before proceeding.
- **Clarify when needed:** If the task description is vague, ask targeted questions rather than guessing.

### Detailed Instructions

#### Phase 1: Assessment

1. Ask the user to describe the long-running task their agent handles.
2. **Identify the target agent:** Ask which agent needs the harness. If multiple agents need it, process them one at a time. Resolve the target agent's entry from `agents.list[]` in `openclaw.json` and its workspace directory path from the `workspace` field (e.g., `{project-root}/agents/{agent-id}/`).
3. If the user has an existing workspace, load and review for the target agent:
   - `openclaw.json` — current heartbeat config at `agents.list[].heartbeat` (agent-specific) or `agents.defaults.heartbeat` (global)
   - `{agent-workspace}/AGENTS.md` — current agent instructions
   - `{agent-workspace}/HEARTBEAT.md` — existing heartbeat instructions (if any)
   - `memory/` — existing progress logs (if any)
4. Determine the task profile:
   - **Duration class:** Single long session (hours) vs multi-session (days/weeks)
   - **Checkpoint granularity:** How often should progress be saved? (every heartbeat cycle, after each subtask, both)
   - **Autonomy level:** Does the agent work autonomously between sessions or wait for user input?
   - **Recovery needs:** What happens if a session ends mid-task? What context must be restored?
5. Summarize the task profile and confirm with the user before proceeding.

#### Phase 2: Progress Tracking

1. Define the progress log structure in `memory/`:
   - Daily log format: `memory/YYYY-MM-DD.md` (OpenClaw's native daily log format)
   - Progress entries include: task name, current phase, completed items, next steps, blockers
2. Add progress tracking instructions to the target agent's AGENTS.md at `{agent-workspace}/AGENTS.md`:
   - "At the end of each work session, write a progress summary to today's memory log"
   - "At the start of each session, read recent memory logs to restore context"
3. **Isolation rule:** Only modify `{agent-workspace}/AGENTS.md` for the target agent. Do not modify other agents' workspace files.
4. Present the progress log format to the user for confirmation.

#### Phase 3: Heartbeat Checkpointing

1. Determine config scope — if the harness applies to a single agent, configure heartbeat on the agent's entry in `agents.list[]` via `agents.list[].heartbeat`. If it applies to all agents, configure via `agents.defaults.heartbeat`. Ask the user which scope they want.
2. Configure the heartbeat block in `openclaw.json` at the chosen scope:
   ```yaml
   # Per-agent example (agents.list[] entry):
   - id: {agent-id}
     heartbeat:
       every: "30m"          # Checkpoint interval
       activeHours:
         start: "08:00"      # Only run during work hours
         end: "22:00"
       prompt: "Read HEARTBEAT.md. Check progress on current long-running task. Save checkpoint to memory log if work has advanced. Reply HEARTBEAT_OK if nothing needs attention."
       target: "none"        # Silent checkpointing (no user notification)

   # Global default example (agents.defaults):
   agents:
     defaults:
       heartbeat:
         every: "30m"
         ...
   ```
3. Generate `HEARTBEAT.md` at `{agent-workspace}/HEARTBEAT.md` with checkpoint-specific instructions:
   - Check current task progress
   - Write checkpoint to `memory/` if progress has been made since last checkpoint
   - Include: current phase, items completed since last checkpoint, next planned steps
   - If task is blocked or stalled, note the blocker
4. Explain to the user: heartbeat injects cron-style current time into the prompt, so the agent always knows "when" it is during checkpointing.
5. Confirm interval, active hours, and delivery target with the user.

#### Phase 4: Session Bridging

1. Configure compaction for long-running context management. Determine scope — per-agent via `agents.list[].compaction` or global via `agents.defaults.compaction`:
   ```yaml
   # Per-agent or agents.defaults:
   compaction:
     mode: "safeguard"        # Aggressive context management for long sessions
     maxHistoryShare: 0.5     # Reserve half the context for new work
     memoryFlush:
       enabled: true          # Flush to memory before compaction
   ```
2. Add session bridging instructions to the target agent's `{agent-workspace}/AGENTS.md`:
   - "When starting a new session, read the last 3 days of memory logs to restore task context"
   - "Use `memory_search` to find relevant prior work if the task spans more than 3 days"
   - "Never assume prior context — always verify by reading memory logs"
3. Explain safeguard mode: it preserves more context during compaction, preventing loss of critical task state.
4. Confirm compaction settings with the user.
5. **Isolation rule:** Only modify `{agent-workspace}/AGENTS.md` for the target agent.

#### Phase 5: Incremental Work Patterns

1. Based on the task profile, configure one of these patterns:
   - **Linear chunking:** Agent works through a sequential task list, marking items done in progress log
   - **Exploratory chunking:** Agent decides what to work on next based on current state and priorities
   - **Delegated chunking:** Agent uses the `sessions_spawn` tool to break work into parallel sub-sessions
2. Add incremental work instructions to the target agent's `{agent-workspace}/AGENTS.md`:
   - How to decide what to work on in the current session
   - When to stop and checkpoint (context approaching limits, natural breakpoint)
   - How to hand off to the next session
3. If using `sessions_spawn` for delegation, configure sub-agent concurrency. Determine scope — per-agent via `agents.list[].subagents` or global via `agents.defaults.subagents`:
   ```yaml
   # Per-agent or agents.defaults:
   subagents:
     maxConcurrent: 3       # Limit parallel sub-sessions
   ```
4. Present the incremental work pattern to the user and confirm.
5. **Isolation rule:** Only modify `{agent-workspace}/AGENTS.md` for the target agent.

#### Phase 6: Verification

1. Review all generated/modified files for the target agent:
   - `openclaw.json` — heartbeat config (at `agents.list[].heartbeat` or `agents.defaults.heartbeat`), compaction config (at `agents.list[].compaction` or `agents.defaults.compaction`), subagents config if applicable
   - `{agent-workspace}/AGENTS.md` — progress tracking, session bridging, incremental work instructions
   - `{agent-workspace}/HEARTBEAT.md` — checkpoint instructions
   - `memory/` directory structure
2. **Isolation check:** Confirm only the target agent's workspace files were modified. No other agent's workspace directory was touched.
3. Run a mental dry-run: "If the agent starts a new session right now, can it restore context and continue work?"
4. Present the complete harness configuration summary to the user.
5. If the harness needs to be applied to additional agents, offer to repeat Phases 1-6 for the next agent.
6. Offer to run `validate-workspace` to verify consistency.

---

## Data Dependencies

**Required at runtime:**
- User's existing `openclaw.json` (to merge config, or create if new)
- User's existing `AGENTS.md` (to append harness instructions, or create if new)
- Heartbeat configuration schema reference (heartbeat.every, activeHours, prompt, target, ackMaxChars)
- Compaction configuration schema reference (mode, maxHistoryShare, memoryFlush)

**Optional enhancements:**
- Existing `HEARTBEAT.md` (to extend rather than overwrite)
- Existing `memory/` logs (to understand current progress tracking patterns)
- `sessions_spawn` configuration reference (if delegated chunking pattern is used)

---

## Connected Skills

**Leads to:** harden-workspace (harness config is part of production hardening), validate-workspace (verify harness configuration consistency)
**Triggered by:** design-system (natural follow-on when designing agents with long-running tasks)
**Shares context with:** setup-knowledge (memory architecture overlaps with progress tracking), harden-workspace (heartbeat and compaction are hardening concerns)

---

## Success Criteria

- Heartbeat configured with appropriate interval and checkpoint prompt in `openclaw.json`
- `HEARTBEAT.md` created with checkpoint-specific instructions
- Compaction configured in safeguard mode with memory flush enabled
- `AGENTS.md` updated with progress tracking, session bridging, and incremental work instructions
- `memory/` directory structure ready for progress logs
- User can describe a scenario where the agent recovers from a session interruption and continues work
- Configuration validated against OpenClaw schema (no invalid keys or values)
