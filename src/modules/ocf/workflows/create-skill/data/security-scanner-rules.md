# Security Best Practices for Skill Authors

This document provides security guidelines for writing and reviewing OpenClaw skills. These are code review recommendations, not an automated scanner. Skill authors and reviewers should use these as a checklist when evaluating skill code.

## Scope

These guidelines apply to executable code in a skill's `scripts/` directory. Common file types include `.js`, `.ts`, `.py`, `.sh`, `.bash`, and their variants.

The SKILL.md body itself contains Markdown instructions for the AI agent and is not executable code.

---

## Critical Patterns to Watch For

These patterns indicate serious security concerns and should be flagged during review.

| Pattern | What to Look For | Why It Matters |
|---------|-----------------|----------------|
| Shell execution in JS/TS | `exec(`, `execSync(`, `spawn(`, `spawnSync(` with `child_process` import | Skill scripts should not spawn arbitrary shell commands; the AI agent handles command execution |
| Dynamic code execution | `eval()` or `new Function()` in any language | Allows arbitrary code injection; almost never necessary |
| Crypto-mining indicators | References to `stratum+tcp`, `stratum+ssl`, `coinhive`, `cryptonight`, `xmrig` | Obvious malicious intent |
| Environment harvesting | `process.env` (or `os.environ`) combined with network requests (`fetch`, `http.request`, `requests.post`) | Could exfiltrate credentials or API keys |

## Warning-Level Patterns

These patterns are not necessarily malicious but deserve scrutiny during review.

| Pattern | What to Look For | Why It Matters |
|---------|-----------------|----------------|
| Unexpected network access | WebSocket connections to non-standard ports, or outbound HTTP to unknown hosts | Could be data exfiltration or command-and-control |
| File read + network send | File reading (`readFileSync`, `open()`) combined with network requests in the same file | Could exfiltrate local file contents |
| Obfuscated code | Long hex-encoded strings (`\xNN` sequences), large Base64 payloads being decoded | Hides true intent of the code |

---

## Guidelines for Skill Authors

### DO

- Use the SKILL.md body to document shell commands the AI agent should run, rather than executing them from script code
- Keep scripts focused on data transformation, formatting, or computation
- Use well-known packages from established registries for complex operations
- Document any legitimate use of flagged patterns in the SKILL.md body
- Prefer JSON.parse() over eval() for parsing data

### DO NOT

- Use `eval()` or `new Function()` in JavaScript/TypeScript skill code
- Use `child_process` functions (exec, spawn) in JS/TS skill scripts
- Access environment variables and make network requests in the same file
- Include long hex-encoded or Base64-encoded strings in code
- Connect to WebSocket servers on undocumented or non-standard ports

### If a Flagged Pattern Is Truly Necessary

1. Document the specific use case in the SKILL.md body
2. Explain why the flagged pattern is required and what alternatives were considered
3. Keep the scope as narrow as possible -- isolate the pattern to a single, small file
4. Expect reviewers to examine the usage carefully

### Preferred Alternatives

| Instead of... | Use... |
|--------------|--------|
| `exec()` in JS scripts | Document the shell command in SKILL.md; let the AI agent run it |
| `eval()` | `JSON.parse()` for data, pre-computed values, or template literals |
| `process.env` + network in one file | Separate concerns: config module for env, separate module for network |
| Obfuscated strings | Plain text with comments explaining the data |

---

## Built-in Validation via package_skill.py

The `package_skill.py` script (located at `skills/skill-creator/scripts/package_skill.py`) runs structural validation before packaging a skill into a `.skill` file. This validation checks:

- SKILL.md exists and has valid YAML frontmatter
- Only allowed frontmatter keys are present (`name`, `description`, `license`, `allowed-tools`, `metadata`)
- The `name` field is valid kebab-case (max 64 characters)
- The `description` field meets format constraints (max 1024 characters, no angle brackets)

This validation focuses on structural correctness, not security scanning. Security review of skill code remains a manual process guided by the patterns described in this document.

---

## Review Checklist Summary

When reviewing a skill before installation or distribution:

1. Read the SKILL.md frontmatter and body for completeness and clarity
2. Check `scripts/` for any executable code
3. Scan for critical patterns (shell execution, eval, crypto-mining, env harvesting)
4. Review warning patterns (unexpected network access, file+network combos, obfuscation)
5. Verify that any flagged patterns are documented and justified in SKILL.md
6. Run `package_skill.py` to confirm structural validation passes
