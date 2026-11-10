---
version: 2
name: cross-cutting-schema-instances-not-mutated-store-6fbf
description: "Core Registries Module for Schema Metadata and Traversal Management: Schema Instances Not Mutated Store Traversal"
metadata:
  actual:
    adr_id: 6fbfbc6b-760e-4276-a2b4-1ea8d005f849
    status: accepted
    candidate_group_id: 030063b8-d655-44ea-bf21-c6f9f8fd93bf
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Core Registries Module for Schema Metadata and Traversal Management: Schema Instances Not Mutated Store Traversal

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema transformation pipelines, schema serialization and generation modules, and internal API schema instance registries.

### Rules

- **R-REG-001** MUST_NOT: Schema instances MUST NOT be mutated to store traversal state, cycle detection tokens, or processing artifacts.

### Verify

```bash
# Discover and run the project test suite covering core schema transformation and registry operations.
# Discover and run the repository static analysis and type checking verification scripts.
```

**Accept when:**
- All core schema transformation tests pass without circular reference errors.
- Static analysis confirms that metadata resolution and traversal state operations use the designated registries and context APIs.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration test and static analysis suites enforce compliance.
</enforcement>