---
version: 2
name: cross-cutting-before-introducing-modifying-code-that-dcca
description: "Internal Core Module Adoption for Schema Traversal and Transformation: Before Introducing Modifying Code That Depends"
metadata:
  actual:
    adr_id: dccaf60f-b070-4825-a5f2-9ee6d22c7fa3
    status: accepted
    candidate_group_id: 64424c11-2cbc-426e-8f54-ae38ba571b66
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module Adoption for Schema Traversal and Transformation: Before Introducing Modifying Code That Depends

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ICM-001** MUST: Before introducing or modifying code that depends on versioned dependencies, consumers MUST inspect the repository lock artifact to determine the exact resolved dependency version and verify API availability against official documentation.
- **R-ICM-002** MUST: Locate the internal core module traversal exports and utility interfaces before implementing new schema transformation capabilities.
- **R-ICM-003** MUST: Verify that dialect-specific transformation functions delegate recursive structural inspection to the core visitor interface while providing dialect-appropriate replacement schemas.

### Verify

```bash
# Discover and run the project test suite from the repository manifest to verify schema transformation consistency across all dialect modules.
# Discover and execute the project static analysis and lint checks to confirm module dependency boundaries.
```

**Accept when:**
- All schema transformation and traversal tests pass across both full and lightweight dialect implementations.
- Module boundary analysis confirms unidirectional dependencies from dialect transformation modules to the internal core module.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>