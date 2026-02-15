# Scaffold Resource Directory Guide

Reference for creating skill resource directories. Each directory type serves a different purpose.

## scripts/

Executable code (Python/Bash) for deterministic, repeatable operations. Use when the same code would be rewritten each time.

**For each script, gather from user:**
- What it does (purpose)
- What language (Python/Bash recommended)
- Input/output expectations

**After generating each script, IMMEDIATELY validate against scanner rules:**
- Check for `eval()`, `new Function()` -- CRITICAL
- Check for `exec()`, `spawn()` with child_process -- CRITICAL
- Check for `process.env` + network requests -- CRITICAL
- Check for hex-encoded strings -- WARNING
- Check for large Base64 payloads -- WARNING

If violations found, discuss alternatives per the security rules. If violations are intentional, document them explicitly.

## references/

Documentation loaded into context on demand. Good for:
- API documentation
- Schema definitions
- Domain knowledge
- Workflow guides

Create reference files collaboratively with user.

## assets/

Files used in output, not loaded into context. Good for:
- Templates
- Icons/images
- Boilerplate code
- Sample documents

User may need to provide some asset files directly.
