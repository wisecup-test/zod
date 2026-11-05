---
version: 2
name: cross-cutting-fs-module-adoption-filesystem-operations-ea6c
description: "node:fs Module Adoption for Filesystem Operations: Filesystem Modules Not Utilize Prefixed Core"
metadata:
  actual:
    adr_id: ea6ce049-7408-4fd6-bb96-fbba9a68f615
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

# node:fs Module Adoption for Filesystem Operations: Filesystem Modules Not Utilize Prefixed Core

Scope: applies to `packages/tsc/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for repository automation scripts, code generators, and verification routines requiring direct host filesystem access and build-time manifest inspection and artifact generation workflows.

### Rules

- **R-FS-001** MUST_NOT: Filesystem modules MUST NOT utilize un-prefixed core module specifiers to prevent namespace collision with external registry packages.

### Verify

```bash
# Discover and execute the repository verification script that checks manifest integrity.
# Discover and run the build generation pipeline to confirm all generated artifacts match the declared schema.
```

**Accept when:**
- All build scripts and code generators import filesystem capabilities through the explicit node:fs protocol specifier without resolution errors.
- Manifest inspection workflows successfully load and parse target configuration files synchronously without unhandled exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis and continuous integration checks will fail on un-prefixed core module imports or asynchronous operations in synchronous script paths.
</enforcement>