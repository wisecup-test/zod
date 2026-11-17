---
version: 2
name: cross-cutting-schema-transformations-query-contextual-3d9a
description: "Internal Core Library Module Decomposition and Registry Pattern in Zod: Schema Transformations Query Contextual Visited Cache"
metadata:
  actual:
    adr_id: 3d9a7a27-8d2a-43cc-b8a3-067eaa004409
    status: accepted
    candidate_group_id: fd8d8f66-6b2f-4c03-8911-bd9f1e5e7e6f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Internal Core Library Module Decomposition and Registry Pattern in Zod: Schema Transformations Query Contextual Visited Cache

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all internal modules within the core library package responsible for schema definitions, validation checks, registry lookups, and schema transformations.

### Rules

- **R-MOD-001** MUST: Schema transformations MUST query the contextual visited cache prior to processing subschemas to prevent unbounded recursion on cyclic structures.
- **R-MOD-002** MUST: Discover the dependency manifest in the repo to identify exact resolved versions before writing code that uses a versioned library, verifying APIs via documentation.
- **R-MOD-003** MUST: Maintain clear layering between schema definition primitives, validation checks, and serialization processors to prevent circular module dependencies.
- **R-MOD-004** MUST: Ensure the contextual traversal cache is initialized at the root of every recursive traversal and forwarded across all child processing operations.
- **R-MOD-005** MUST: Keep global registries focused on instance lookup and metadata resolution rather than transient execution state.

### Verify

\`\`\`bash
# Discover and execute the repository test runner to validate recursive schema generation, registry lookups, and serialization behaviors.
# Discover and execute the repository module boundary and circular dependency verification scripts to ensure import isolation between core submodules.
# Discover and execute the repository static type checker to verify internal interface compatibility across all core module boundaries.
\`\`\`

**Accept when:**
- All core module interfaces and internal imports resolve through the defined module boundaries without circular module initialization errors.
- Schema transformations and serializations correctly track cyclic structures using the contextual traversal cache without memory leaks.
- Static type checking and automated regression suites pass completely across all core library components.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>