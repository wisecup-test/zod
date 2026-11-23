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

These rules are ALWAYS ACTIVE for:
- Core schema transformation pipelines
- Schema serialization and generation modules
- Internal API schema instance registries

### Rules

- **R-LM-001** MUST: Consumers MUST discover the project dependency lock artifact and verify resolved versions before implementing or extending modular interfaces.

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
