# Forge Validation Checklist

## Structural Checks

### Workspace Files

| File | Required | Expected Sections |
|------|----------|-------------------|
| SOUL.md | Yes | Identity, personality, communication style, lore |
| AGENTS.md | Yes | Agent capabilities, tool policies, boundaries |
| IDENTITY.md | Yes | Name, role, expertise, forge metaphors |

### Skill Files (All 9 Required)

| Skill | File Pattern | Required Elements |
|-------|-------------|-------------------|
| design-system | SKILL.md | Trigger examples, flow description, output specification |
| add-agent | SKILL.md | Trigger examples, flow description, output specification |
| recommend-pattern | SKILL.md | Trigger examples, flow description, output specification |
| setup-knowledge | SKILL.md | Trigger examples, flow description, output specification |
| setup-harness | SKILL.md | Trigger examples, flow description, output specification |
| harden-workspace | SKILL.md | Trigger examples, flow description, output specification |
| validate-workspace | SKILL.md | Trigger examples, flow description, output specification |
| export-package | SKILL.md | Trigger examples, flow description, output specification |
| import-package | SKILL.md | Trigger examples, flow description, output specification |

### Reference Data Files

| File | Required | Purpose |
|------|----------|---------|
| Agentic patterns library | Yes | 7 patterns with OpenClaw implementation guides |
| Config schema reference | Yes | OpenClaw configuration field definitions |

### Module Configuration

| File | Required | Expected Fields |
|------|----------|-----------------|
| module.yaml | Yes | code, name, header, subheader, forge_artifacts variable |

---

## Coherence Checks

### Cross-Reference Rules

| Rule | Source | Target | Check |
|------|--------|--------|-------|
| CR-01 | module-brief skill list | Actual skill files | Every skill in brief has a corresponding file |
| CR-02 | Skill pattern references | Patterns library | Every pattern referenced in skills exists in library |
| CR-03 | Skill config references | Config schema | Every config field referenced in skills exists in schema |
| CR-04 | Agent name in IDENTITY.md | SOUL.md, AGENTS.md | Name consistent across all workspace files |
| CR-05 | Workflow connections in brief | Actual workflow files | Every workflow referenced in brief exists |
| CR-06 | Skill trigger examples | Other skills | No overlapping triggers between skills |
| CR-07 | Personality traits in SOUL.md | IDENTITY.md | Personality consistent across files |

---

## Completeness Checks

### Skills Completeness (9 Required)

**Core Skills (3):**
1. design-system
2. add-agent
3. recommend-pattern

**Feature Skills (3):**
4. setup-knowledge
5. setup-harness
6. harden-workspace

**Utility Skills (3):**
7. validate-workspace
8. export-package
9. import-package

### BMAD Build Workflows (5 Required)

1. build-forge-agent
2. build-forge-skill
3. update-reference-data
4. package-forge
5. validate-forge

### Agentic Patterns (7 Required)

1. Prompt Chaining
2. Routing
3. Parallelization
4. Orchestrator-Workers
5. Evaluator-Optimizer
6. Autonomous Agent
7. Long-Running Harness

### Bundled Resources Per Skill

Each skill should have:
- SKILL.md with trigger examples, flow, and output spec
- Any referenced templates or data files bundled

---

## Verdict Criteria

| Verdict | Condition |
|---------|-----------|
| PASS | 0 failures, 0 warnings |
| PASS WITH WARNINGS | 0 failures, >0 warnings |
| FAIL | >0 failures |
