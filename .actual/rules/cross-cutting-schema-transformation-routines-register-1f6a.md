---
version: 2
name: cross-cutting-schema-transformation-routines-register-1f6a
description: "Zod Core JSON Schema Transformation Modules: Schema Transformation Routines Register Query Visited"
metadata:
  actual:
    adr_id: 1f6aad21-3553-4d3e-83dc-4adf83a67959
    status: accepted
    candidate_group_id: bf562f7e-2eba-4e98-a358-82c1dab13f6c
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Zod Core JSON Schema Transformation Modules: Schema Transformation Routines Register Query Visited

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for core schema transformation and JSON Schema generation modules within the library, context management, schema processor registries, and metadata lookup implementations.

### Rules

- **R-ZOD-001** MUST: Schema transformation routines MUST register and query visited schemas in the traversal context cache via seen lookups to prevent infinite recursion and duplicate processing.

### Verify

```bash
# Discover and execute the test runner targeting core schema conversion modules
# Discover and execute workspace static analysis and linting scripts to verify boundary compliance
```

**Accept when:**
- The repository test suite executes without failures across all JSON Schema generation scenarios, including recursive and circular definitions.
- Static boundary checks confirm schema transformation processors only interact with core registries through the context interface.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>