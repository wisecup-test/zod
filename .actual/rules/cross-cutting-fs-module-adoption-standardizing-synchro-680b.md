---
version: 2
name: cross-cutting-fs-module-adoption-standardizing-synchro-680b
description: "node:fs Module Adoption: Standardizing Synchronous File System Access in Repository Automation Scripts: File Read Operations Targeting Text Structured"
metadata:
  actual:
    adr_id: 680b5cb2-5a9c-43ad-8820-299d16ca4b5c
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

# node:fs Module Adoption: Standardizing Synchronous File System Access in Repository Automation Scripts: File Read Operations Targeting Text Structured

Scope: applies to `.claude/skills/triage/scripts/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for standalone repository maintenance, triage, verification, and code generation scripts, and local file system inspection and artifact writing workflows executed outside of published distribution packages.

### Rules

- **R-FS-001** MUST: File read operations targeting text and structured data files MUST specify explicit character encoding when invoking node:fs read methods.

### Verify

```bash
# Discover the project verification script defined in the repository configuration manifest and execute it to verify repository integrity.
# Inspect script source files to confirm all file system imports utilize the protocol-prefixed core module namespace without third-party wrapper dependencies.
```

**Accept when:**
- All repository automation and verification scripts execute to completion without file system resolution errors.
- Static module import analysis confirms file system access in script files is restricted to the protocol-qualified core module namespace.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>