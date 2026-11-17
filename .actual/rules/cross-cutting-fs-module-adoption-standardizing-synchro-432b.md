---
version: 2
name: cross-cutting-fs-module-adoption-standardizing-synchro-432b
description: "node:fs Module Adoption: Standardizing Synchronous File System Access in Repository Automation Scripts: Sequential Verification Artifact Generation Scripts Employ"
metadata:
  actual:
    adr_id: 432baac2-86ad-4cbc-8e4d-b8e910e01a9a
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

# node:fs Module Adoption: Standardizing Synchronous File System Access in Repository Automation Scripts: Sequential Verification Artifact Generation Scripts Employ

Scope: applies to `.claude/skills/triage/scripts/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for standalone repository maintenance, triage, verification, and code generation scripts executed outside of published distribution packages.

### Rules

- **R-FS-001** SHOULD: Sequential verification and artifact generation scripts SHOULD employ synchronous read operations such as readFileSync for discrete metadata inspection to ensure deterministic and linear execution flow.
- **R-FS-002** MANDATORY: When reading structured data files, pass the text encoding parameter directly to readFileSync prior to parsing the decoded string.
- **R-FS-003** MANDATORY: Wrap file system read operations in structured exception handling blocks to emit informative diagnostic messages upon file absence or access failure.

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