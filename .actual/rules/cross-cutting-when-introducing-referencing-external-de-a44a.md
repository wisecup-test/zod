---
version: 2
name: cross-cutting-when-introducing-referencing-external-de-a44a
description: "Zod Core JSON Schema Transformation Modules: When Introducing Referencing External Dependencies Within"
metadata:
  actual:
    adr_id: a44aa409-9bc7-4d4f-ac7b-4982fe174ede
    status: accepted
    candidate_group_id: bf562f7e-2eba-4e98-a358-82c1dab13f6c
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Zod Core JSON Schema Transformation Modules: When Introducing Referencing External Dependencies Within

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for core schema transformation and JSON Schema generation modules within the library, including context management, schema processor registries, and metadata lookup implementations.

### Rules

- **R-ZOD-001** MUST: When introducing or referencing external dependencies within schema processing modules, consumers MUST inspect the repository lock artifact and verify the exact resolved dependency version before integration.

### Verify

```bash
# Discover and execute the test runner targeting core schema conversion modules
# Discover and execute workspace static analysis and linting scripts to verify module dependency boundaries
```

**Accept when:**
- The repository test suite executes without failures across all JSON Schema generation scenarios, including recursive and circular definitions.
- Static boundary checks confirm schema transformation processors only interact with core registries through the context interface.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>