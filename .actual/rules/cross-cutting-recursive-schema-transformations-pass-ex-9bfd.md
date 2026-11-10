---
version: 2
name: cross-cutting-recursive-schema-transformations-pass-ex-9bfd
description: "Internal Core Library Module Decomposition and Registry Pattern in Zod: Recursive Schema Transformations Pass Execution Context"
metadata:
  actual:
    adr_id: 9bfd7300-f262-46b7-a6b0-ae281b753704
    status: accepted
    candidate_group_id: fd8d8f66-6b2f-4c03-8911-bd9f1e5e7e6f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Internal Core Library Module Decomposition and Registry Pattern in Zod: Recursive Schema Transformations Pass Execution Context

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all internal modules within the core library package responsible for schema definitions, validation checks, registry lookups, and schema transformations, as well as functions performing recursive schema graph analysis, serialization, or metadata aggregation.

### Rules

- **R-CORE-001** MUST: Recursive schema transformations MUST pass an execution context containing a visited cache to record and resolve circular or repeated schema instances.

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
Claude Code MUST NOT skip or defer verification. Compliance is verified by automated static analysis, module boundary linting, comprehensive test suites, and mandatory peer code review.
</enforcement>