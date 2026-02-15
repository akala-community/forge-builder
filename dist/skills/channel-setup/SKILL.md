---
name: channel-setup
description: Generate a platform-specific channel layout plan and implementation configuration for a Forge workspace, mapping each agent to a dedicated channel with proper categories, naming, and per-channel welcome/instruction content.
category: feature
version: 1.0.0
---

# Channel Setup

## Triggers

**Activation phrases and patterns:**

- "set up channels for my workspace"
- "configure discord channels for my agents"
- "channel setup"
- "create channel plan for my agents"
- "set up discord for my forge workspace"
- "map agents to channels"
- "create a channel layout"
- "configure communication channels"
- "how should I organize channels for my agents"
- "set up agent channels on [platform]"

**Trigger logic:**
- Primary triggers: "channel", "channels", "discord" combined with agent/workspace/setup references
- Contextual triggers: After `equip-agents` completes (agents have tools bound, now need communication channels), or after `design-system` Phase 3 (agent roster confirmed). The Forge detects agents without channel assignments and offers to set them up. Also activates when a user asks "where do my agents communicate?" or "how do users interact with each agent?"

---

## Execution Flow

**Overview:** Read the agent roster, determine the target channel platform, generate a categorized channel layout mapping each agent to a dedicated channel with naming conventions and welcome content, then output a complete channel setup document.

### Step-by-step flow:

1. **Load Agent Roster** — Read the workspace's agent definitions to identify all agents, their roles, and communication patterns
   - Input: Agent roster from `design-system` output, `add-agent` specs, or AGENTS.md
   - Output: Agent list with roles, responsibilities, and interaction patterns
   - User interaction: "Let me inspect your agent roster to plan the channel layout."

2. **Select Channel Provider** — Ask the user which platform they're deploying channels on
   - Input: User preference
   - Output: Selected platform (Discord initially, extensible to Slack, Teams, etc.)
   - User interaction: "Which platform are you using for agent channels? Currently I support Discord, with more platforms coming."

3. **Generate Channel Plan** — Propose categories, channel names, and agent-to-channel mapping based on the roster
   - Input: Agent roster + selected platform
   - Output: Channel plan with categories, channel names following platform naming conventions, and agent-to-channel assignments
   - User interaction: "Here's the proposed channel layout. Each agent gets a dedicated channel, organized into categories by function."

4. **Review and Iterate** — Present the plan for user feedback and adjust
   - Input: Generated channel plan + user feedback
   - Output: User-confirmed channel plan
   - User interaction: "Review the layout. Want to rename any channels, reorganize categories, or adjust agent assignments?"

5. **Generate Per-Channel Configuration** — For each channel, produce descriptions, welcome messages, and agent invocation instructions
   - Input: Confirmed channel plan
   - Output: Per-channel config: description text, welcome/pinned message content, agent invocation instructions (e.g., `@AgentName` for Discord), channel topic text
   - User interaction: "Generating welcome messages and invocation instructions for each channel."

6. **Output Channel Setup Document** — Compile the complete channel configuration as a manual setup guide or automation-ready config
   - Input: All confirmed channel configurations
   - Output: Channel setup document with full layout, per-channel details, and setup instructions
   - User interaction: "Here's your complete channel setup document. Follow the setup guide to create channels on [platform], or use the automation script."

7. **Generate Automation Script (Optional)** — If user requests, produce a platform-specific script to create channels programmatically
   - Input: Channel setup document + platform API details
   - Output: Platform-specific automation script (e.g., Discord bot script using discord.js)
   - User interaction: "Want me to generate an automation script to create these channels via the [platform] API?"

---

## Instructions

### Role

The Forge activates this skill as a **Channel Architect** — the specialist who designs the communication infrastructure for a multi-agent workspace. Maps each agent to its own channel with clear naming, organized categories, and per-channel instructions so users know exactly how to interact with each agent. "Every agent needs a front door. Let me build yours."

### Behavior Guidelines

- **Roster-driven:** Always start from the actual agent roster. Don't propose channels for agents that don't exist, and don't skip agents that do.
- **Platform-aware:** Respect platform naming conventions (Discord: lowercase, hyphens, no spaces; Slack: similar). Apply character limits and formatting rules.
- **Convention consistent:** Use a consistent naming pattern across all channels (e.g., `agent-{role}` or `{category}-{function}`). Let the user choose the convention.
- **Welcome content specific:** Each channel's welcome message must include the specific agent's name, role description, example commands or prompts, and any usage instructions unique to that agent.
- **Collaborative on layout:** Present the proposed layout, but the user decides final organization. If they want to merge channels, split categories, or rename things, adjust without pushback.
- **Clarification triggers:** Ask when: multiple agents could share a channel (should they?), when the roster has agents with overlapping communication roles, or when the user's preferred platform has channel count limits.

### Detailed Instructions

#### Phase 1: Roster Analysis

1. Read the agent roster from the most recent `design-system` output, `add-agent` spec, or AGENTS.md in the workspace.
2. For each agent, extract:
   - Agent name and role
   - Primary responsibilities (what users would contact this agent for)
   - Communication style (from agent persona — informs welcome message tone)
   - Tools and capabilities (from `equip-agents` output if available — informs what the agent can do in-channel)
3. Build the agent-channel mapping matrix:
   | Agent | Role | Proposed Channel | Category |
   |-------|------|-----------------|----------|
4. Present the matrix to the user for validation.
5. If the roster isn't available, ask the user to describe their agents or run `design-system` first.

#### Phase 2: Platform Configuration

1. Confirm target platform with the user.
2. Apply platform-specific rules:
   - **Discord:** Channel names lowercase with hyphens, max 100 chars. Categories supported. Channel topics limited to 1024 chars. Welcome messages via pinned messages or bot auto-response. Roles for agent mentions.
   - **Future platforms:** Extensible pattern — platform rules loaded from data file when available.
3. Determine channel structure:
   - How many categories (group agents by function: core, feature, utility, admin, etc.)
   - Whether to include shared channels (e.g., `#general`, `#agent-updates`, `#system-logs`)
   - Whether agents share any channels or are strictly 1:1

#### Phase 3: Channel Plan Generation

1. Generate the channel plan:
   ```
   ## Category: {Category Name}

   ### #{channel-name}
   - **Agent:** {Agent Name}
   - **Purpose:** {What this channel is for}
   - **Topic:** {Channel topic text — max platform limit}
   ```
2. Include shared/system channels if appropriate:
   - `#welcome` — workspace overview and getting started
   - `#system-status` — agent health, heartbeat, and system notifications
   - `#admin` — workspace administration and configuration
3. Present the complete plan for review.
4. Iterate until the user confirms.

#### Phase 4: Per-Channel Content Generation

1. For each channel, generate:
   - **Channel description:** 1-2 sentence explanation of the channel's purpose
   - **Welcome message:** Agent introduction, role description, example usage, and invocation instructions. Written in the agent's communication style where possible.
   - **Pinned instructions:** How to interact with the agent in this channel (commands, mention syntax, expected input format)
   - **Topic text:** Compact channel topic for the header bar
2. Example welcome message format:
   ```
   Welcome to #{channel-name}

   This channel is home to **{Agent Name}** — {role description}.

   **What I can help with:**
   - {Capability 1}
   - {Capability 2}
   - {Capability 3}

   **How to use this channel:**
   - Mention @{AgentName} followed by your request
   - Example: "@{AgentName} {example prompt}"

   **Tips:**
   - {Usage tip relevant to this agent}
   ```
3. Present all welcome messages for review.

#### Phase 5: Document Assembly

1. Compile the complete channel setup document:
   - **Channel Layout Overview** — visual category/channel tree
   - **Per-Channel Details** — full config for each channel (name, description, topic, welcome message, agent binding)
   - **`bindings[]` Configuration** — generate the corresponding `bindings[]` entries for `openclaw.json` that route each channel to its assigned agent. Each binding must include `agentId` (matching `agents.list[].id`) and `match` with the appropriate `channel` value. Present the config for user review before applying.
   - **Setup Checklist** — ordered steps to create channels on the target platform
   - **Role/Permission Recommendations** — which roles to create for agent mentions, channel access controls
   - **Integration with equip-agents** — how channel setup relates to tool bindings (MCP servers may need channel context)
2. Write the channel setup document to `{forge_artifacts}/channel-setup-{workspaceName}.md`.
3. Present summary with next steps.

---

## Data Dependencies

**Required at runtime:**
- Agent roster from `design-system`, `add-agent`, or AGENTS.md (who the agents are and what they do)
- Workspace name/identity (for naming conventions and document output)

**Optional enhancements:**
- `equip-agents` tool plan output (enriches channel descriptions with concrete tool capabilities)
- Platform API access (for automation script generation — Discord bot token, etc.)
- Existing channel configuration (if migrating or updating an existing channel setup)
- Agent persona/communication style details (for tone-matched welcome messages)

---

## Connected Skills

**Leads to:** `harden-workspace` (channel config used for approval forwarding and notification targets), `plan-operations` (channel config used for heartbeat targets and operational notifications), `validate-workspace` (verify channel assignments match agent roster)
**Triggered by:** `design-system` Phase 3 (agent roster confirmed — natural follow-on), `equip-agents` (after tools are bound, channels are the next infrastructure layer), standalone user request
**Shares context with:** `equip-agents` (tool bindings inform channel capability descriptions), `harden-workspace` (channel config feeds into notification and approval routing), `plan-operations` (channel config used for heartbeat targets), `setup-harness` (long-running agent channels may need special configuration)

---

## Success Criteria

- Every agent in the roster is mapped to a dedicated channel
- Channel names follow platform naming conventions consistently
- Categories organize channels logically by agent function
- Each channel has a complete welcome message with agent introduction, capabilities, and invocation instructions
- Channel setup document is complete with layout, per-channel details, and setup checklist
- User confirmed the channel plan before content generation
- Connected skills referenced accurately (leads to, triggered by, shares context)
- Optional automation script offered for programmatic channel creation
