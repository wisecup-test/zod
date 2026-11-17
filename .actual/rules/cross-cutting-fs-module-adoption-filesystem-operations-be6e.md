---
version: 2
name: cross-cutting-fs-module-adoption-filesystem-operations-be6e
description: "node:fs Module Adoption for Filesystem Operations: Raw Data Retrieved Through Filesystem Read"
metadata:
  actual:
    adr_id: be6ecda8-487a-4460-b102-064eafd8672f
    status: accepted
    candidate_group_id: 94b4be7d-f692-465c-af7a-c152e660ebb3
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/tsc/**
      - scripts/**
---

# node:fs Module Adoption for Filesystem Operations: Raw Data Retrieved Through Filesystem Read

Scope: applies to `packages/tsc/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for all repository automation scripts, code generators, and verification routines requiring direct host filesystem access.

### Rules

- **R-FS-001** MUST: Raw data retrieved through filesystem read operations MUST undergo structured parsing or input validation immediately following ingestion.

### Verify

```bash
# Discover and execute the repository verification script that checks manifest integrity.
# Discover and run the build generation pipeline to confirm all generated artifacts match the declared schema.
```

**Accept when:**
- All build scripts and code generators import filesystem capabilities through the explicit node:fs protocol specifier without resolution errors.
- Manifest inspection workflows successfully load and parse target configuration files synchronously without unhandled exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>