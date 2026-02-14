# TODO: OpenClaw Forge (OCF)

Development roadmap for ocf module.

---

## Agents to Build

- [ ] forge-master (Lead Architect & Brief Creator)
  - Use: `bmad:bmb:agents:agent-builder`
  - Spec: `agents/forge-master.spec.md`

- [ ] soul-smith (Persona & Identity Designer)
  - Use: `bmad:bmb:agents:agent-builder`
  - Spec: `agents/soul-smith.spec.md`

- [ ] gear-wright (Skills, Config & Assembly Engineer)
  - Use: `bmad:bmb:agents:agent-builder`
  - Spec: `agents/gear-wright.spec.md`

---

## Workflows to Build

### Core Workflows

- [ ] create-agent-brief
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/create-agent-brief/create-agent-brief.spec.md`

- [ ] create-agent-system
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/create-agent-system/create-agent-system.spec.md`

- [ ] create-single-agent
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/create-single-agent/create-single-agent.spec.md`

### Feature Workflows

- [ ] design-orchestration
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/design-orchestration/design-orchestration.spec.md`

- [ ] create-skill
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/create-skill/create-skill.spec.md`

- [ ] edit-agent-system
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/edit-agent-system/edit-agent-system.spec.md`

- [ ] configure-production-hardening
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/configure-production-hardening/configure-production-hardening.spec.md`

### Utility Workflows

- [ ] validate-workspace
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/validate-workspace/validate-workspace.spec.md`

- [ ] export-config
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/export-config/export-config.spec.md`

- [ ] package-export
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/package-export/package-export.spec.md`

- [ ] package-import
  - Use: `bmad:bmb:workflows:workflow` or `/workflow`
  - Spec: `workflows/package-import/package-import.spec.md`

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

_Last updated: 2026-02-11_
