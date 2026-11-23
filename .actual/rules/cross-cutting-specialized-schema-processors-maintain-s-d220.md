---
version: 2
name: cross-cutting-specialized-schema-processors-maintain-s-d220
description: "Core Registries Module for Schema Metadata and Traversal Management: Specialized Schema Processors Maintain Secondary Pattern"
metadata:
  actual:
    adr_id: d220814a-6c65-4278-ba52-8dca4900fd8d
    status: accepted
    candidate_group_id: 030063b8-d655-44ea-bf21-c6f9f8fd93bf
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Core Registries Module for Schema Metadata and Traversal Management: Specialized Schema Processors Maintain Secondary Pattern

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for:
- Core schema transformation pipelines
- Schema serialization and generation modules
- Internal API schema instance registries

### Rules

- **R-LM-001** MAY: Specialized schema processors MAY maintain secondary pattern or rewrite caches within the execution context to accelerate exact pattern matching.

### Verify

- Discover and run the project test suite covering core schema transformation and registry operations.
- Discover and run the repository static analysis and type checking verification scripts.

**Accept when:**

- All core schema transformation tests pass without circular reference errors.
- Static analysis confirms that metadata resolution and traversal state operations use the designated registries and context APIs.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration test and static analysis suites
- Verified by: Peer code review for core schema processing pull requests
- Violation handling: Pull requests mutating schema instances or bypassing registries are blocked from merging
- Violation handling: Flagged violations must be refactored to use context registries
- Exception process: Submit an architectural review request detailing why context registry usage is technically infeasible for the specific transform.
</enforcement>
