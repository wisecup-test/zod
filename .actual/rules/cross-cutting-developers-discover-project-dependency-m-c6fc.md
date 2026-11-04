---
version: 2
name: cross-cutting-developers-discover-project-dependency-m-c6fc
description: "Internal Core Library Module Decomposition and Registry Pattern in Zod: Developers Discover Project Dependency Manifest Lock"
metadata:
  actual:
    adr_id: c6fc8352-0cb3-4399-87d4-3261103fd6a4
    status: accepted
    candidate_group_id: fd8d8f66-6b2f-4c03-8911-bd9f1e5e7e6f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Internal Core Library Module Decomposition and Registry Pattern in Zod: Developers Discover Project Dependency Manifest Lock

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all internal modules within the core library package responsible for schema definitions, validation checks, registry lookups, and schema transformations, as well as functions performing recursive schema graph analysis, serialization, or metadata aggregation.

### Rules

- **R-ZOD-001** MUST: Developers MUST discover the project dependency manifest and lock resolution artifact to identify exact resolved versions before implementing or modifying library dependencies.

### Verify

```bash
# Discover and execute the repository test runner to validate recursive schema generation, registry lookups, and serialization behaviors.
# Discover and execute the repository module boundary and circular dependency verification scripts to ensure import isolation between core submodules.
# Discover and execute the repository static type checker to verify internal interface compatibility across all core module boundaries.
```

**Accept when:**
- All core module interfaces and internal imports resolve through the defined module boundaries without circular module initialization errors.
- Schema transformations and serializations correctly track cyclic structures using the contextual traversal cache without memory leaks.
- Static type checking and automated regression suites pass completely across all core library components.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated static analysis, module boundary linting, code reviews, and unit/integration test suites.
</enforcement>