---
version: 2
name: cross-cutting-schema-processors-return-serialized-repr-1def
description: "Zod Core JSON Schema Transformation Modules: Schema Processors Return Serialized Representations Derived"
metadata:
  actual:
    adr_id: 1def4916-451e-40d3-9ad9-9ffbe5163625
    status: accepted
    candidate_group_id: bf562f7e-2eba-4e98-a358-82c1dab13f6c
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Zod Core JSON Schema Transformation Modules: Schema Processors Return Serialized Representations Derived

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for core schema transformation and JSON Schema generation modules within the library, context management, schema processor registries, and metadata lookup implementations.

### Rules

- **R-ZOD-001** SHOULD: Schema processors SHOULD return serialized representations derived through immutable structural cloning when handling default values.

### Verify

```bash
# Discover the repository configuration to locate and execute the test runner targeting core schema conversion modules.
# Discover the workspace static analysis and linting scripts to verify compliance with internal module dependency boundaries.
```

**Accept when:**
- The repository test suite executes without failures across all JSON Schema generation scenarios, including recursive and circular definitions.
- Static boundary checks confirm schema transformation processors only interact with core registries through the context interface.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>