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

These rules are ALWAYS ACTIVE for core schema transformation pipelines, schema serialization and generation modules, and internal API schema instance registries.

### Rules

- **R-CORE-001** MAY: Specialized schema processors MAY maintain secondary pattern or rewrite caches within the execution context to accelerate exact pattern matching.
- **R-CORE-002** MANDATORY (DISCOVERY POLICY): Omit all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.
- **R-CORE-003** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, find the dependency manifest, identify the build tool, inspect the repository lock or resolution artifact, look up official documentation for that exact version, confirm every API/class/function exists, and re-run per dependency at point of use.
- **R-CORE-004** MANDATORY: Instantiate execution context instances at the root of schema processing and pass the context reference to all downstream visitors.
- **R-CORE-005** MANDATORY: Ensure identity registries use reference-equality data structures to prevent unintended duplicate entries for equivalent schema definitions.

### Verify

```bash
# Discover and run the project test suite covering core schema transformation and registry operations.
# Discover and run the repository static analysis and type checking verification scripts.
```

**Accept when:**
- All core schema transformation tests pass without circular reference errors.
- Static analysis confirms that metadata resolution and traversal state operations use the designated registries and context APIs.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration test, static analysis suites, and peer code reviews enforce compliance.
</enforcement>