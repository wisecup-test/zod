---
version: 2
name: cross-cutting-transformation-pipelines-pass-contextual-3c16
description: "Core Registries Module for Schema Metadata and Traversal Management: Transformation Pipelines Pass Contextual Metadata Registries"
metadata:
  actual:
    adr_id: 3c160d02-8c1b-4e68-9da1-17d5cfb3ae68
    status: accepted
    candidate_group_id: 030063b8-d655-44ea-bf21-c6f9f8fd93bf
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Core Registries Module for Schema Metadata and Traversal Management: Transformation Pipelines Pass Contextual Metadata Registries

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema transformation pipelines, schema serialization and generation modules, and internal API schema instance registries.

### Rules

- **R-COR-001** SHOULD: Transformation pipelines SHOULD pass contextual metadata registries such as metadataRegistry through execution contexts to preserve schema encapsulation.
- **R-COR-002** MANDATORY: Discover the project test suite covering core schema transformation and registry operations, and run it.
- **R-COR-003** MANDATORY: Discover the repository static analysis and type checking verification scripts, and run them.

### Verify

```bash
# Discover and run test suite for core schema transformation and registry operations
# Discover and run static analysis and type checking scripts
```

**Accept when:**
- All core schema transformation tests pass without circular reference errors.
- Static analysis confirms that metadata resolution and traversal state operations use the designated registries and context APIs.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration test and static analysis suites, as well as peer code reviews, verify compliance.
</enforcement>