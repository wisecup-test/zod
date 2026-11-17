---
version: 2
name: cross-cutting-consumers-discover-project-dependency-lo-dd01
description: "Core Registries Module for Schema Metadata and Traversal Management: Consumers Discover Project Dependency Lock Artifact"
metadata:
  actual:
    adr_id: dd019c9c-4b9c-4adc-9063-248a77caf967
    status: accepted
    candidate_group_id: 030063b8-d655-44ea-bf21-c6f9f8fd93bf
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Core Registries Module for Schema Metadata and Traversal Management: Consumers Discover Project Dependency Lock Artifact

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for core schema transformation pipelines, schema serialization and generation modules, and internal API schema instance registries.

### Rules

- **R-CORE-001** MUST: Consumers MUST discover the project dependency lock artifact and verify resolved versions before implementing or extending modular interfaces.
- **R-CORE-002** MUST: Execute lock-version grounding steps in order (find manifest, identify build tool, inspect lock/resolution artifact, lookup official documentation for exact version, confirm APIs exist, re-run per dependency at point of use) before writing code that uses a versioned library.
- **R-CORE-003** MUST: Instantiate execution context instances at the root of schema processing and pass the context reference to all downstream visitors.
- **R-CORE-004** MUST: Ensure identity registries use reference-equality data structures to prevent unintended duplicate entries for equivalent schema definitions.

### Verify

```bash
# Discover and run the project test suite covering core schema transformation and registry operations
# Discover and run the repository static analysis and type checking verification scripts
```

**Accept when:**
- All core schema transformation tests pass without circular reference errors.
- Static analysis confirms that metadata resolution and traversal state operations use the designated registries and context APIs.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration test and static analysis suites as well as peer code review for core schema processing pull requests.
</enforcement>