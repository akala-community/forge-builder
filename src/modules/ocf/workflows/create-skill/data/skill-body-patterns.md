# Skill Body Patterns

Reference patterns for writing SKILL.md body content. Use the appropriate pattern based on what the skill wraps.

## CLI Tool Wrapper

```markdown
# {Skill Title}

Use the `{tool}` CLI to {purpose}. {Any critical context}.

## {Primary Use Case}

{Concise example with code block}

## {Secondary Use Case}

{Concise example with code block}

## {Additional sections as needed}
```

## API-Based Skill

```markdown
# {Skill Title}

{Brief description of the API and authentication}.

## {Primary Operation}

{Code example or instruction}

## Configuration

{Required env vars, config, etc.}
```

## Knowledge-Based Skill

```markdown
# {Skill Title}

{Domain knowledge and workflow instructions}

## {Workflow Step 1}

{Instructions}

## {Workflow Step 2}

{Instructions}
```

## Bundled Resources References

If the skill has bundled resources, include these sections as needed:

```markdown
## Scripts

- `scripts/{name}.py` -- {purpose}. Run with: `python scripts/{name}.py {args}`

## References

- See [reference.md](references/reference.md) for {topic}

## Assets

- Template at `assets/{name}` -- {how to use}
```

## Progressive Disclosure

For complex skills exceeding 500 lines, apply progressive disclosure:
- Keep core workflow in SKILL.md
- Move detailed reference material to references/ files
- Include clear links: "See [DETAILS.md](references/DETAILS.md) for complete API reference"
