# Getting Started with OCF: The Forge

Welcome to forge! This guide will help you get up and running.

---

## What This Module Does

The Forge is a meta-agent that designs, builds, configures, and deploys multi-agent AI systems on OpenClaw. It takes Anthropic's proven agentic patterns (prompt chaining, routing, parallelization, orchestrator-workers, evaluator-optimizer, autonomous agents, long-running harnesses) and turns them into one-conversation implementations.

Users go from "I have an idea" to a running, hardened, knowledge-connected multi-agent system without editing a single config file.

---

## Installation

If you haven't installed the module yet:

```bash
bmad install forge
```

Follow the prompts to configure the module for your needs.

---

## First Steps

1. **Talk to The Forge** — Open your preferred channel (WhatsApp, Telegram, Discord, TUI) and describe the system you need
2. **Let The Forge design** — It will analyze your use case, recommend an agentic pattern, and design an agent roster
3. **Review and deploy** — The Forge generates all workspace files and config, validates everything, and guides deployment

---

## Common Use Cases

### Build a Multi-Agent Team
"I want a customer support system with a triage agent and three specialist agents"
- The Forge selects the Routing pattern, designs the agents, generates workspace files and bindings

### Add an Agent to an Existing System
"Add a research agent that my main agent can delegate to"
- The Forge reads your existing workspace, designs the new agent, merges configuration

### Set Up Knowledge Architecture
"My agents should remember customer context across conversations"
- The Forge configures tiered memory: flat-file, vector, or knowledge graph depending on your needs

### Harden for Production
"Make my agents production-ready"
- Systematic hardening checklist: memory config, tool policies, failover, observability, boundaries

---

## What's Next?

- Check out the [Agents Reference](agents.md) to meet your team
- Browse the [Workflows Reference](workflows.md) to see what you can do
- See [Examples](examples.md) for real-world usage

---

## Need Help?

If you run into issues:
1. Check the troubleshooting section in examples.md
2. Review your module configuration
3. Consult the broader BMAD documentation
