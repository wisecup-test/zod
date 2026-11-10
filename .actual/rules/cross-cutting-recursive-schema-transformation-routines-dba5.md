---
version: 2
name: cross-cutting-recursive-schema-transformation-routines-dba5
description: "Core Registries Module for Schema Metadata and Traversal Management: Recursive Schema Transformation Routines Register Check"
metadata:
  actual:
    adr_id: dba52763-d39c-4ea5-bc61-accc7e2803d5
    status: accepted
    candidate_group_id: 030063b8-d655-44ea-bf21-c6f9f8fd93bf
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Core Registries Module for Schema Metadata and Traversal Management: Recursive Schema Transformation Routines Register Check

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for core schema transformation pipelines, schema serialization and generation modules, and internal API schema instance registries.

### Rules

- **R-CORE-001** MUST: Recursive schema transformation routines MUST register and check visited schema references in a contextual traversal cache such as ctx.seen to prevent circular recursion.

### Verify

```bash
# Discover and run the project test suite covering core schema transformation and registry operations.
# Discover and run the repository static analysis and type checking verification scripts.
```

**Accept when:**
- All core schema transformation tests pass without circular reference errors.
- Static analysis confirms that metadata resolution and traversal state operations use the designated registries and context APIs.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration test and static analysis suites, and peer code review.
</enforcement>