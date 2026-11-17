---
version: 2
name: cross-cutting-fs-module-adoption-filesystem-operations-2790
description: "node:fs Module Adoption for Filesystem Operations: Repository Scripts Build Generators Import Filesystem"
metadata:
  actual:
    adr_id: 27906d61-1308-449b-8859-0982f51de95d
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

# node:fs Module Adoption for Filesystem Operations: Repository Scripts Build Generators Import Filesystem

Scope: applies to `packages/tsc/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for repository automation scripts, code generators, verification routines, and build-time manifest inspection workflows.

### Rules

- **R-FS-001** MUST: Repository scripts and build generators MUST import filesystem capabilities exclusively via the explicit node:fs protocol specifier.

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