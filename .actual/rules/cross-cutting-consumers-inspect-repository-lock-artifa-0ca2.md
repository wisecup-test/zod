---
version: 2
name: cross-cutting-consumers-inspect-repository-lock-artifa-0ca2
description: "Core Module Architecture for Validation Engine and Global Registry Management: Consumers Inspect Repository Lock Artifact Verify"
metadata:
  actual:
    adr_id: 0ca2cf97-b2f9-4133-a116-58755d9f1455
    status: accepted
    candidate_group_id: d439e3f0-eafd-4b71-a843-e881f89e04eb
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/**
---

# Core Module Architecture for Validation Engine and Global Registry Management: Consumers Inspect Repository Lock Artifact Verify

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for:
- Implementation and extension of validation schemas, checks, and error structures.
- Registration and resolution of schema metadata within internal registries.
- Integration of schema transformation processors and legacy compatibility adapters.

### Rules

- **R-LM-001** MUST: Consumers MUST inspect the repository lock artifact to verify the exact resolved version of any external library dependency before authoring or integrating module-level consumers.

### Verify

- Discover and run the project static analysis and linting command to verify module boundary compliance.
- Discover and execute the project test runner across core module test suites.
- Discover and execute the circular dependency checker script defined in the project configuration.

**Accept when:**

- All core module test suites complete with zero errors.
- Static dependency validation passes without detecting disallowed inward imports into the core module layer.
- Schema registry resolution tests verify deterministic cache lookups across compatibility facades.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated dependency graph validation and static lint checks executed in continuous integration pipelines.
- Verified by: Peer code review mandatory for any changes altering core module interfaces or registry structures.
- Violation handling: Pull requests introducing backward dependencies into core modules or circumventing the global registry are automatically blocked.
- Violation handling: Architectural violations must be refactored to comply with core module boundaries prior to merge approval.
- Exception process: Exceptions require formal architectural review and written consensus from library maintainers documenting why the dependency boundary cannot be maintained.
</enforcement>
