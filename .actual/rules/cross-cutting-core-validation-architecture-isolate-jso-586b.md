---
version: 2
name: cross-cutting-core-validation-architecture-isolate-jso-586b
description: "Zod Core JSON Schema Transformation Modules: Core Validation Architecture Isolate Json Schema"
metadata:
  actual:
    adr_id: 586bbef5-54fc-4bbc-887a-6c6eb84d628c
    status: accepted
    candidate_group_id: bf562f7e-2eba-4e98-a358-82c1dab13f6c
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Zod Core JSON Schema Transformation Modules: Core Validation Architecture Isolate Json Schema

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MUST: The core validation architecture MUST isolate JSON Schema translation into modular processors coordinated through an explicit traversal context.

### Verify

```bash
# Discover and execute the test runner targeting core schema conversion modules
# Discover and execute workspace static analysis and linting scripts
```

**Accept when:**
- The repository test suite executes without failures across all JSON Schema generation scenarios, including recursive and circular definitions.
- Static boundary checks confirm schema transformation processors only interact with core registries through the context interface.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>