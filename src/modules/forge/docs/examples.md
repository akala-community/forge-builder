# Examples & Use Cases

This section provides practical examples for using OCF: The Forge.

---

## Example Workflows

### Building a Customer Support System

**User:** "I want to build a customer support system with a triage agent and three specialists — billing, technical, and general inquiries."

**The Forge:**
1. Analyzes the use case — distinct input categories needing specialist handling
2. Recommends **Routing pattern** — bindings with match rules route to specialists
3. Designs 4 agents: Triage Router, Billing Specialist, Technical Specialist, General Specialist
4. Generates workspace files for each agent (SOUL.md, AGENTS.md, etc.)
5. Generates openclaw.json with bindings, model config, tool policies
6. Offers knowledge graph setup for customer context memory
7. Validates the complete system
8. Packages for deployment

### Building a Research Team

**User:** "I need a research team that can break down complex topics, investigate in parallel, and synthesize findings."

**The Forge:**
1. Analyzes the use case — complex tasks with unpredictable subtasks
2. Recommends **Orchestrator-Workers pattern** — coordinator spawns specialist workers
3. Designs agents: Research Coordinator, Topic Investigators (spawned dynamically)
4. Configures `sessions_spawn` for parallel investigation
5. Sets up knowledge graph for accumulating research findings

---

## Common Scenarios

### Adding an Agent to an Existing System

"Add a fact-checker agent that reviews everything before it goes to the user."

The Forge reads your existing workspace, designs the new agent as an **Evaluator-Optimizer** gate, generates its workspace files, and merges config — preserving everything that already works.

### Setting Up Long-Running Tasks

"My research agent needs to work across multiple sessions on big topics."

The Forge configures the **Long-Running Harness** pattern — progress logging in memory/, heartbeat checkpointing, session bridging so work continues across context resets.

### Hardening for Production

"My agents are working but I want them production-ready."

The Forge runs a systematic checklist:
- Memory configuration review
- Tool policy lockdown
- Model failover (primary + fallbacks)
- Observability (heartbeat monitoring)
- Self-correction (AGENTS.md guardrails)
- Boundaries (SOUL.md + sandbox restrictions)

---

## Tips & Tricks

- **Start with `recommend-pattern`** if you're unsure what architecture you need — The Forge will explain trade-offs before committing
- **Use `validate-workspace`** after any changes — catches inconsistencies early
- **Knowledge graphs compound** — the more your agents interact, the smarter they get
- **Export frequently** — `export-package` creates snapshots you can roll back to

---

## Troubleshooting

### Common Issues

**"The Forge doesn't recognize my existing workspace"**
- Ensure your OpenClaw workspace has a valid openclaw.json at the root
- Check that workspace files are in the expected locations

**"Generated config has validation errors"**
- Run `update-reference-data` to sync The Forge's config reference with your OpenClaw version
- Then regenerate the config

**"Knowledge graph setup fails"**
- Verify MCP server connectivity (neo4j-mcp or memory server)
- Check that mcporter skill is available in your OpenClaw instance

---

## Getting More Help

- Review the main BMAD documentation
- Check module configuration in module.yaml
- Verify all agents and workflows are properly installed
