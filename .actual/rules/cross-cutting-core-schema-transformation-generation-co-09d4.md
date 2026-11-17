---
version: 2
name: cross-cutting-core-schema-transformation-generation-co-09d4
description: "Core Registries Module for Schema Metadata and Traversal Management: Core Schema Transformation Generation Components Use"
metadata:
  actual:
    adr_id: 09d455a5-50b6-43ed-b5cc-108662f0e2f8
    status: accepted
    candidate_group_id: 030063b8-d655-44ea-bf21-c6f9f8fd93bf
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Core Registries Module for Schema Metadata and Traversal Management: Core Schema Transformation Generation Components Use

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema transformation pipelines, schema serialization and generation modules, and internal API schema instance registries.

### Rules

- **R-REG-001** MUST: Core schema transformation and generation components MUST use the internal registries module for global schema registration and metadata resolution.

### Verify

```bash
# Discover and run the project test suite covering core schema transformation and registry operations.
# Discover and run the repository static analysis and type checking verification scripts.
```

**Accept when:**
- All core schema transformation tests pass without circular reference errors.
- Static analysis confirms that metadata resolution and traversal state operations use the designated registries and context APIs.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>