---
name: setup-knowledge
description: Tiered memory architecture setup — assess needs, recommend tier, configure backend, set up hooks, verify
category: feature
version: 1.0.0
---

# Setup Knowledge

## Triggers

**Activation phrases and patterns:**

- "set up memory"
- "knowledge graph"
- "agents should remember..."
- "I want my agents to share knowledge"
- "set up long-term memory"
- "add memory to my system"
- "configure knowledge for my agents"
- "memory architecture"
- "persistent memory"
- "agents need to learn over time"

**Trigger logic:**
- Primary triggers: Explicit requests for memory, knowledge, or remembering capabilities
- Contextual triggers: After `design-system` completes, The Forge offers knowledge setup as a natural follow-on; mentions of "context", "history", or "learning" in combination with agent discussions

---

## Execution Flow

**Overview:** Assess the user's memory needs, recommend the appropriate tier (flat-file, vector, or graph), configure the chosen backend, set up auto-capture/recall hooks, and verify the architecture works end-to-end.

### Step-by-step flow:

1. **Assess Needs** — Understand what the user's agents need to remember and why
   - Input: Current workspace configuration, agent roster, user description of memory requirements
   - Output: Memory requirements profile (what to store, access patterns, retention, cross-agent sharing needs)
   - User interaction: "What should your agents remember? Tell me about the kind of knowledge they need to accumulate — customer details, past decisions, research findings, conversation history?"

2. **Recommend Tier** — Match requirements to the appropriate memory tier
   - Input: Memory requirements profile
   - Output: Recommended tier with justification
   - User interaction: Present tier comparison with trade-offs, explain why the recommended tier fits their needs, get confirmation

   **Tier Decision Matrix:**

   | Tier | Backend | Best For | Complexity |
   |------|---------|----------|------------|
   | Flat-file | `memory/` daily logs + `memory_search` (sqlite-vec) | Session history, simple recall, single-agent setups | Low |
   | Vector | `memory_search` with embedding provider | Semantic search across large content, similarity matching | Medium |
   | Graph | Neo4j via `neo4j-mcp` or `@modelcontextprotocol/server-memory` | Entity relationships, structured knowledge, multi-agent shared understanding | High |

3. **Configure Backend** — Set up the chosen memory backend
   - Input: Confirmed tier selection, workspace configuration
   - Output: Backend configuration added to workspace
   - User interaction: Guide through any required setup (API keys for embeddings, Neo4j connection, MCP server config)

   **Per-tier configuration:**
   - **Flat-file:** Configure `memory/` directory structure, set up `memorySearch.provider` in openclaw.json
   - **Vector:** Configure embedding provider (OpenAI, Gemini, Voyage, or Local), set similarity thresholds, configure `memorySearch` block
   - **Graph:** Configure MCP server connection (Neo4j or memory-server), set up `mcporter` skill binding, define schema (entity types, relationship types)

4. **Set Up MCP (If Graph Tier)** — Connect MCP servers for graph-tier knowledge
   - Input: Graph backend choice (Neo4j or memory-server)
   - Output: MCP server configured and connected via `mcporter`
   - User interaction: "I'll connect the knowledge graph server. Do you have Neo4j running, or should we use the lightweight memory server?"

   **Neo4j path:** Configure `neo4j-mcp` server, set connection URI, credentials, database name
   **Memory-server path:** Configure `@modelcontextprotocol/server-memory`, set storage location

5. **Configure Hooks** — Set up auto-capture and auto-recall hooks
   - Input: Configured backend, agent roster
   - Output: Hook configurations in workspace
   - User interaction: "I'll set up automatic knowledge capture and recall. Your agents will extract entities after each conversation and inject relevant context before each turn."

   **Hook setup:**
   - `before_agent_start` hook: Query knowledge backend for relevant context based on incoming message, inject as system context
   - `agent_end` hook: Extract entities, relationships, and key facts from conversation, store in knowledge backend
   - Configure hook scope (which agents, which channels)

6. **Verify** — Test the knowledge architecture end-to-end
   - Input: Complete configuration
   - Output: Verification report
   - User interaction: "Let me run the quality inspection on your knowledge architecture — checking connections, hooks, and data flow."

   **Verification checks:**
   - Backend connectivity (can read/write)
   - Hook registration (hooks fire correctly)
   - Data flow (capture -> store -> recall cycle)
   - Cross-agent sharing (if multi-agent: Agent A captures, Agent B recalls)
   - Configuration consistency with workspace

---

## Instructions

### Role

The Forge activates this skill as a **Knowledge Architect** — designing and deploying the memory layer that gives agents persistent, structured understanding. This is "the memory anvil" — where raw conversation data is shaped into lasting knowledge.

### Behavior Guidelines

- **Collaborative:** Always explain the trade-offs between tiers before recommending. Never force a tier choice — the user understands their data best.
- **Progressive disclosure:** Start with the simple question ("what should your agents remember?") and layer in technical details as decisions narrow. Don't front-load complexity.
- **Autonomy level:** Medium — The Forge recommends and explains, but the user confirms tier selection and any external service choices (Neo4j vs memory-server, embedding provider).
- **Error handling:** If a backend connection fails during verification, diagnose clearly and offer alternatives. Never leave the user with a broken configuration.
- **Clarification triggers:** Ask when the user's requirements could fit multiple tiers equally well, when external service access is unclear, or when cross-agent sharing patterns are ambiguous.

### Detailed Instructions

#### Phase 1: Discovery

1. Read the current workspace to understand the agent roster and existing configuration.
2. Ask the user what their agents need to remember. Listen for:
   - **Data types:** Customer info, research findings, decisions, conversation history, project state
   - **Access patterns:** Frequent recall vs archival, keyword vs semantic vs relationship-based
   - **Retention:** Short-term (session) vs long-term (persistent across sessions)
   - **Sharing:** Single-agent vs multi-agent shared knowledge
3. Synthesize into a memory requirements profile.
4. If coming from `design-system`, leverage the system design context — you already know the agents, their roles, and communication patterns.

#### Phase 2: Tier Selection

1. Present the three-tier comparison table with the user's specific needs mapped to each tier.
2. Make a clear recommendation with reasoning:
   - **Flat-file** if: Single agent, session history is sufficient, no complex relationships needed
   - **Vector** if: Need semantic search across large content, similarity-based recall, single or few agents
   - **Graph** if: Entity relationships matter, multi-agent shared understanding, structured knowledge that compounds
3. Wait for user confirmation before proceeding.
4. If the user is unsure, offer to start with a lower tier and explain the upgrade path.

#### Phase 3: Backend Configuration

1. **Flat-file tier:**
   - Ensure `memory/` directory exists in workspace
   - Configure `memorySearch` in openclaw.json with appropriate provider
   - Set search parameters (result count, similarity threshold)

2. **Vector tier:**
   - Configure embedding provider in `memorySearch.provider`
   - If provider needs API key, guide user through setup
   - Set `memorySearch.topK` and similarity thresholds
   - Configure auto-embedding for memory entries

3. **Graph tier:**
   - Ask user: Neo4j (full graph database) or memory-server (lightweight JSON-based)?
   - **Neo4j:** Configure `neo4j-mcp` in mcporter config — URI, auth, database
   - **Memory-server:** Configure `@modelcontextprotocol/server-memory` — storage path
   - Define knowledge schema: entity types relevant to the use case, relationship types
   - Set up `mcporter` skill binding so agents can query the graph

#### Phase 4: Hook Configuration

1. Design the `before_agent_start` hook:
   - Determine what context to inject (recent entities, related knowledge, user profile)
   - Configure query parameters (how many results, relevance threshold)
   - Scope to appropriate agents (not all agents may need knowledge injection)

2. Design the `agent_end` hook:
   - Define entity extraction rules (what to capture from conversations)
   - Configure relationship detection (how entities connect)
   - Set deduplication strategy (merge vs create new)
   - Scope to appropriate agents

3. If using the Plugin SDK for knowledge-graph extension:
   - Register tools and hooks via the plugin interface
   - Configure plugin settings in workspace

#### Phase 5: Verification

1. Test backend connectivity — read and write a test entry
2. Test hook registration — verify hooks are configured and will fire
3. Test the full cycle: simulate a conversation, verify capture, verify recall
4. If multi-agent: verify cross-agent knowledge sharing
5. Present verification report with pass/fail for each check
6. If any check fails: diagnose, fix, re-verify

---

## Data Dependencies

**Required at runtime:**
- Memory tier comparison data (decision matrix for tier recommendation)
- OpenClaw config schema (for generating valid `memorySearch` and `mcporter` configuration)
- Hook configuration templates (for `before_agent_start` and `agent_end` hooks)

**Optional enhancements:**
- Knowledge schema templates (pre-built entity/relationship schemas for common use cases)
- MCP server setup guides (Neo4j installation, memory-server setup)
- Example configurations from past deployments (via The Forge's own `memory_search`)

---

## Connected Skills

**Leads to:** `harden-workspace` (memory configuration is part of the hardening checklist), `validate-workspace` (verify knowledge architecture integrity)
**Triggered by:** `design-system` (natural follow-on — "Want your agents to remember?"), standalone user request
**Shares context with:** `design-system` (agent roster, workspace config), `harden-workspace` (memory hardening section), `setup-harness` (long-running tasks may use memory for progress persistence)

---

## Success Criteria

- User's memory requirements are understood and documented
- Appropriate tier is recommended with clear justification
- Backend is configured and connectivity verified
- Hooks are configured for auto-capture and auto-recall
- Full capture-store-recall cycle verified working
- Cross-agent sharing verified (if applicable)
- Configuration is consistent with existing workspace
- User confirms the knowledge architecture meets their needs
