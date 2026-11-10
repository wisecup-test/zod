---
version: 2
name: cross-cutting-transformation-processors-normalize-defa-84ba
description: "Internal Core Library Module Decomposition and Registry Pattern in Zod: Transformation Processors Normalize Default Value Definitions"
metadata:
  actual:
    adr_id: 84ba8f4d-9f7c-4f7f-9a12-f94e9eaad38b
    status: accepted
    candidate_group_id: fd8d8f66-6b2f-4c03-8911-bd9f1e5e7e6f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Internal Core Library Module Decomposition and Registry Pattern in Zod: Transformation Processors Normalize Default Value Definitions

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all internal modules within the core library package responsible for schema definitions, validation checks, registry lookups, and schema transformations, as well as functions performing recursive schema graph analysis, serialization, or metadata aggregation.

### Rules

- **R-ZOD-001** MAY: Transformation processors MAY normalize default value definitions and serialization artifacts through structured deep cloning mechanisms when immutability guarantees are required.
- **R-ZOD-002** MANDATORY: Discover and execute the repository test runner to validate recursive schema generation, registry lookups, and serialization behaviors.
- **R-ZOD-003** MANDATORY: Discover and execute the repository module boundary and circular dependency verification scripts to ensure import isolation between core submodules.
- **R-ZOD-004** MANDATORY: Discover and execute the repository static type checker to verify internal interface compatibility across all core module boundaries.
- **R-ZOD-005** MANDATORY: Enforce unidirectional internal module import hierarchies and verify lack of circular references through automated linting and dependency tree analysis.
- **R-ZOD-006** MANDATORY: Scope traversal caches strictly to the lifecycle of individual transformation requests to prevent memory leakage across concurrent or repeated operations.
- **R-ZOD-007** MANDATORY: Maintain clear layering between schema definition primitives, validation checks, and serialization processors to prevent circular module dependencies.
- **R-ZOD-008** MANDATORY: Ensure the contextual traversal cache is initialized at the root of every recursive traversal and forwarded across all child processing operations.
- **R-ZOD-009** MANDATORY: Keep global registries focused on instance lookup and metadata resolution rather than transient execution state.

### Verify

```bash
# Discover and execute the repository test runner
# Discover and execute the repository module boundary and circular dependency verification scripts
# Discover and execute the repository static type checker
```

**Accept when:**
- All core module interfaces and internal imports resolve through the defined module boundaries without circular module initialization errors.
- Schema transformations and serializations correctly track cyclic structures using the contextual traversal cache without memory leaks.
- Static type checking and automated regression suites pass completely across all core library components.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests containing direct circular module imports or bypassed registry context structures are blocked from merging.
</enforcement>