# Examples & Use Cases

This section provides practical examples for using OpenClaw Forge.

---

## Example Workflows

### Building a Customer Support System

**Scenario:** You want three agents -- a triage agent that routes inquiries, a technical support agent, and a billing agent.

1. Activate **Vulcan** and use `[AB] Create Agent Brief`
2. Describe your system: "I need a customer support system with triage, tech support, and billing agents across WhatsApp and Discord"
3. Vulcan guides you through:
   - Defining each agent's role and responsibilities
   - Mapping skills (knowledge base lookup, ticket creation, billing API access)
   - Designing routing: triage agent receives all messages, classifies, and spawns the appropriate specialist
   - Planning memory: triage agent tracks routing accuracy, specialists track resolution patterns
   - Setting resilience: failover to a general support agent if specialists are unavailable
4. Brief complete -- hand off to **Anima** for persona design
5. Anima crafts each agent's voice, boundaries, and self-correction patterns
6. **Cog** assembles everything: skills, config, tool policies (billing agent gets no shell access), memory scaffolds
7. Review, refine, package, deploy

### Creating a Solo Research Assistant

**Scenario:** You need a single research agent for personal use.

1. Activate **Anima** and use `[SA] Create Single Agent`
2. Describe: "A research assistant that helps me explore topics, summarize papers, and maintain a knowledge base"
3. Anima handles everything in one streamlined flow -- persona, skills, config, assembly
4. Done in one session

---

## Common Scenarios

### Adding Production Hardening to an Existing Workspace

You have an OpenClaw workspace that works but lacks production features.

1. Activate **Cog** and use `[PH] Production Hardening`
2. Point Cog at your workspace path
3. Cog assesses what's missing and adds:
   - Memory backend configuration
   - Tool policies per agent
   - Failover chains
   - Self-correction directives
   - Boundary rules

### Sharing Your Agent System

You've built something great and want a colleague to use it.

1. Activate **Cog** and use `[PE] Package Export`
2. Cog bundles your workspace into `my-system.ocf.zip` + `my-system.setup.md`
3. Send both files to your colleague
4. They send the zip + prompt to their OpenClaw agent, which self-installs everything

---

## Tips & Tricks

- **Start with the brief** -- Even if you think you know what you want, the brief workflow surfaces considerations you might miss (memory architecture, failure handling, tool policies)
- **Use single-agent for prototyping** -- Start with create-single-agent to validate an idea, then expand to a full system later
- **Run validation after edits** -- Any time you manually modify a generated workspace, run validate-workspace to catch coherence issues
- **Production hardening works on any workspace** -- Not just OCF-generated ones. Use it on existing OpenClaw setups too

---

## Troubleshooting

### Common Issues

**"Brief is missing information"**
The create-agent-brief workflow validates completeness. If prompted for missing details, provide them -- the quality of your generated workspace depends on the quality of the brief.

**"Workspace validation failures"**
After generation or editing, run validate-workspace. Common issues include:
- Skills referenced in AGENTS.md but not present in skills/
- Tool policies not defined for all agents
- Memory directives missing for agents with sidecar needs

**"Package import fails"**
Ensure the receiving OpenClaw instance has write access to the workspace directories. Check that the openclaw.json merge doesn't conflict with existing agent entries.

---

## Getting More Help

- Review the main BMAD documentation
- Check module configuration in module.yaml
- Verify all agents and workflows are properly installed
