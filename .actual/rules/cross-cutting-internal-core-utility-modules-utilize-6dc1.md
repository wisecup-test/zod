---
version: 2
name: cross-cutting-internal-core-utility-modules-utilize-6dc1
description: "Core Module Architecture for Validation Engine and Global Registry Management: Internal Core Utility Modules Utilize Reflection"
metadata:
  actual:
    adr_id: 6dc167aa-6e95-40cc-8a95-8e5ca857a314
    status: accepted
    candidate_group_id: d439e3f0-eafd-4b71-a843-e881f89e04eb
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/**
---

# Core Module Architecture for Validation Engine and Global Registry Management: Internal Core Utility Modules Utilize Reflection

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for:
- Implementation and extension of validation schemas, checks, and error structures.
- Registration and resolution of schema metadata within internal registries.
- Integration of schema transformation processors and legacy compatibility adapters.

### Rules

- **R-LM-001** MAY: Internal core utility modules MAY utilize reflection proxies when coordinating dynamic property resolution across schema instance boundaries.

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
