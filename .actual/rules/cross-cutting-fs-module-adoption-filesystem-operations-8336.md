---
version: 2
name: cross-cutting-fs-module-adoption-filesystem-operations-8336
description: "node:fs Module Adoption for Filesystem Operations: Filesystem Read Operations During Script Execution"
metadata:
  actual:
    adr_id: 83360311-a28f-4b6e-895f-77640d3ff486
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

# node:fs Module Adoption for Filesystem Operations: Filesystem Read Operations During Script Execution

Scope: applies to `packages/tsc/**`, `scripts/**`.

These rules are ALWAYS ACTIVE for repository automation scripts, code generators, and verification routines requiring direct host filesystem access.

### Rules

- **R-FS-001** MUST: Filesystem read operations during script execution and artifact generation MUST invoke readFileSync with explicit character encoding to guarantee deterministic data ingestion before downstream processing.
- **R-FS-002** MUST: Import node:fs using protocol-prefixed specifiers across all tooling and generation modules to ensure unambiguous runtime resolution.

### Verify

```bash
# Discover and execute the repository verification script that checks manifest integrity
# Discover and run the build generation pipeline to confirm all generated artifacts match the declared schema
```

**Accept when:**
- All build scripts and code generators import filesystem capabilities through the explicit node:fs protocol specifier without resolution errors.
- Manifest inspection workflows successfully load and parse target configuration files synchronously without unhandled exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis and CI checks enforce these rules.
</enforcement>