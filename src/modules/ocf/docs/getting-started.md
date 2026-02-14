# Getting Started with OpenClaw Forge

Welcome to OCF! This guide will help you get up and running.

---

## What This Module Does

OpenClaw Forge is an end-to-end agent factory for the OpenClaw platform. It transforms your agent system ideas into fully deployable, production-hardened multi-agent workspaces -- complete with personas, directives, skills, configuration, memory scaffolds, and orchestration patterns.

---

## Installation

If you haven't installed the module yet:

```bash
bmad install ocf
```

Follow the prompts to configure the module for your needs.

---

## First Steps

1. **Activate Vulcan (Forge Master)** -- He's your entry point. Start here to describe what you want to build.
2. **Create a brief** -- Use the `[AB] Create Agent Brief` command. Vulcan will guide you through structured discovery of your agent system.
3. **Generate the system** -- Once the brief is complete, Anima (Soul Smith) crafts the identities, and Cog (Gear Wright) assembles everything.
4. **Review and refine** -- Each handoff includes a review gate where you can adjust before proceeding.
5. **Package and deploy** -- Use Cog's packaging commands to bundle your workspace for portable deployment.

---

## Common Use Cases

### Single Agent Creation
You have one agent in mind -- a personal assistant, a code reviewer, a content writer. Use the **create-single-agent** workflow for a streamlined experience that handles brief + generation in one pass.

### Multi-Agent System
You need a team of agents that work together -- customer support triage + specialists, a development team, a content pipeline. Start with **create-agent-brief** to design the full system, then **create-agent-system** to generate everything.

### Production Hardening
You have an existing OpenClaw workspace that needs memory configuration, tool policies, failover chains, and self-correction patterns. Use **configure-production-hardening** -- it works on any workspace, not just OCF-generated ones.

### Sharing Agent Systems
You've built something great and want to share it. Use **package-export** to create a portable `.ocf.zip` + setup prompt that anyone can deploy on their OpenClaw instance.

---

## What's Next?

- Check out the [Agents Reference](agents.md) to meet your forge team
- Browse the [Workflows Reference](workflows.md) to see what you can do
- See [Examples](examples.md) for real-world usage

---

## Need Help?

If you run into issues:
1. Check the troubleshooting section in examples.md
2. Review your module configuration
3. Consult the broader BMAD documentation
