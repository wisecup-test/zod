---
version: 2
name: cross-cutting-schema-traversal-operations-utilize-core-3b1c
description: "Internal Core Module Adoption for Schema Traversal and Transformation: Schema Traversal Operations Utilize Core Visitor"
metadata:
  actual:
    adr_id: 3b1cd6d3-e147-4201-90a0-6993edec4560
    status: accepted
    candidate_group_id: 64424c11-2cbc-426e-8f54-ae38ba571b66
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module Adoption for Schema Traversal and Transformation: Schema Traversal Operations Utilize Core Visitor

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-TRAV-001** SHOULD: Schema traversal operations SHOULD utilize the core visitor interface to perform node inspection and replacement across composite schema structures.
- **R-TRAV-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-TRAV-003** MANDATORY: Before writing code that uses a versioned library, execute in order: (1) Find dependency manifest, (2) Identify build tool, (3) Inspect repository lock/resolution artifact for exact version, (4) Look up official docs/changelog for that exact version, (5) Confirm API existence before calling, (6) Re-run steps 3-5 per dependency at point of use.
- **R-TRAV-004** MANDATORY: Locate internal core module traversal exports and utility interfaces before implementing new schema transformation capabilities.
- **R-TRAV-005** MANDATORY: Verify that dialect-specific transformation functions delegate recursive structural inspection to the core visitor interface while providing dialect-appropriate replacement schemas.

### Verify

```bash
# Discover and run the project test suite from the repository manifest to verify schema transformation consistency across all dialect modules.
# Discover and execute the project static analysis and lint checks to confirm module dependency boundaries and verify that core modules do not depend on dialect submodules.
```

**Accept when:**
- All schema transformation and traversal tests pass across both full and lightweight dialect implementations.
- Module boundary analysis confirms unidirectional dependencies from dialect transformation modules to the internal core module.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration test validation, static analysis checks, and architectural code reviews verify compliance. Violations will be blocked at CI or must be refactored.
</enforcement>