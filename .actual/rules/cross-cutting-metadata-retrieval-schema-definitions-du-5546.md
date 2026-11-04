---
version: 2
name: cross-cutting-metadata-retrieval-schema-definitions-du-5546
description: "Zod Core JSON Schema Transformation Modules: Metadata Retrieval Schema Definitions During Transformation"
metadata:
  actual:
    adr_id: 5546a915-08c6-4e45-a566-459e09469354
    status: accepted
    candidate_group_id: bf562f7e-2eba-4e98-a358-82c1dab13f6c
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Zod Core JSON Schema Transformation Modules: Metadata Retrieval Schema Definitions During Transformation

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema transformation and JSON Schema generation modules within the library.

### Rules

- **R-ZOD-001** MUST: Metadata retrieval for schema definitions during transformation MUST resolve through a dedicated metadata registry interface on the traversal context rather than direct schema inspection.

### Verify

```bash
# Discover and execute the test runner targeting core schema conversion modules based on repository layout
# Discover and execute workspace static analysis and linting scripts to verify module dependency boundaries
```

**Accept when:**
- The repository test suite executes without failures across all JSON Schema generation scenarios, including recursive and circular definitions.
- Static boundary checks confirm schema transformation processors only interact with core registries through the context interface.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>