# TODO: OCF: The Forge — Agentic System Architect

Development roadmap for forge module.

---

## Agents to Build

- [ ] The Forge (Agentic System Architect)
  - Use: `bmad:bmb:agents:agent-builder`
  - Spec: `agents/forge.spec.md`

- [ ] Morgan (Module Lifecycle Manager)
  - Use: `bmad:bmb:agents:agent-builder`
  - Spec: `agents/forge-builder.spec.md`

---

## Workflows to Build

- [ ] build-forge-agent
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/build-forge-agent/build-forge-agent.spec.md`

- [ ] build-forge-skill
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/build-forge-skill/build-forge-skill.spec.md`

- [ ] add-forge-skill
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/add-forge-skill/add-forge-skill.spec.md`

- [ ] update-reference-data
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/update-reference-data/update-reference-data.spec.md`

- [ ] package-forge
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/package-forge/package-forge.spec.md`

- [ ] validate-forge
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/validate-forge/validate-forge.spec.md`

---

## Installation Testing

- [ ] Test installation with `bmad install`
- [ ] Verify module.yaml prompts work correctly
- [ ] Verify all agents and workflows are discoverable

---

## Documentation

- [ ] Complete README.md with usage examples
- [ ] Enhance docs/ folder with more guides
- [ ] Add troubleshooting section
- [ ] Document configuration options

---

## Next Steps

1. Build agents using create-agent workflow
2. Build workflows using create-workflow workflow
3. Test installation and functionality
4. Iterate based on testing

---

_Last updated: 2026-02-13_
