---
version: 2
name: cross-cutting-fs-module-adoption-standardizing-synchro-6ce8
description: "node:fs Module Adoption: Standardizing Synchronous File System Access in Repository Automation Scripts: Automation Scripts Not Introduce Third Party"
metadata:
  actual:
    adr_id: 6ce88fcd-ff8e-48e6-8ce1-7a099022ec91
    status: accepted
    candidate_group_id: f60af43a-94a4-4f74-b47b-742a1e4db0fd
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - .claude/skills/triage/scripts/**
      - scripts/**
---

# node:fs Module Adoption: Standardizing Synchronous File System Access in Repository Automation Scripts: Automation Scripts Not Introduce Third Party

Scope: applies to `.claude/skills/triage/scripts/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-FS-001** MUST_NOT: Automation scripts MUST NOT introduce third-party wrapper libraries for basic file system read and write operations when equivalent capabilities are provided directly by node:fs.

### Verify

```bash
# Discover and execute the project verification script defined in the repository configuration manifest
# Inspect script source files to confirm all file system imports utilize the protocol-prefixed core module namespace
```

**Accept when:**
- All repository automation and verification scripts execute to completion without file system resolution errors.
- Static module import analysis confirms file system access in script files is restricted to the protocol-qualified core module namespace.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>