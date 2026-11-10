---
version: 2
name: cross-cutting-processors-not-maintain-mutable-transfor-5b02
description: "Zod Core JSON Schema Transformation Modules: Processors Not Maintain Mutable Transformation State"
metadata:
  actual:
    adr_id: 5b02eadf-1a40-400e-8468-e75a5830d3ad
    status: accepted
    candidate_group_id: bf562f7e-2eba-4e98-a358-82c1dab13f6c
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Zod Core JSON Schema Transformation Modules: Processors Not Maintain Mutable Transformation State

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema transformation and JSON Schema generation modules within the library.

### Rules

- **R-ZOD-001** MUST NOT: Processors MUST NOT maintain mutable transformation state across separate invocation lifecycles outside the supplied traversal context.

### Verify

```bash
# Discover and run test suites and static analysis per repository configuration for core schema conversion modules
```

**Accept when:**
- The repository test suite executes without failures across all JSON Schema generation scenarios, including recursive and circular definitions.
- Static boundary checks confirm schema transformation processors only interact with core registries through the context interface.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>