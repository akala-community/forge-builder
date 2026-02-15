# .ocf.zip Format Specification

## Overview

The `.ocf.zip` (OpenClaw Format) is a distributable package containing a complete Forge workspace that can be installed into any OpenClaw instance.

## Archive Structure

```
forge-{version}.ocf.zip
├── manifest.json              # Package metadata
├── SETUP.md                   # First-run setup instructions
├── workspace/
│   ├── SOUL.md                # Agent soul/identity document
│   ├── AGENTS.md              # Agent definitions and roles
│   ├── IDENTITY.md            # System identity configuration
│   └── [other workspace files]
├── skills/
│   └── [skill files]          # Generated skill definitions
├── reference/
│   ├── patterns/              # Patterns library
│   └── config/                # Configuration reference
└── RELEASE.md                 # Release notes (optional)
```

## manifest.json Schema

```json
{
  "name": "forge",
  "version": "1.0.0",
  "buildDate": "2026-02-13T00:00:00Z",
  "compatibility": {
    "openclaw": ">=1.0.0"
  },
  "files": [
    {
      "path": "workspace/SOUL.md",
      "type": "workspace",
      "required": true
    }
  ],
  "fileCount": 0,
  "checksum": ""
}
```

## Required Files

| File | Description | Required |
|------|-------------|----------|
| manifest.json | Package metadata | Yes |
| SETUP.md | First-run setup instructions | Yes |
| workspace/SOUL.md | Agent soul document | Yes |
| workspace/AGENTS.md | Agent definitions | Yes |
| workspace/IDENTITY.md | Identity configuration | Yes |

## Verification Checks

1. Archive can be extracted without errors
2. manifest.json is valid JSON
3. All files listed in manifest exist in archive
4. All required files are present
5. File count matches manifest.fileCount
