---
version: 2
name: cross-cutting-compatibility-adapters-external-schema-c-6b7a
description: "Core Module Architecture for Validation Engine and Global Registry Management: Compatibility Adapters External Schema Converters Delegate"
metadata:
  actual:
    adr_id: 6b7a2cdd-0c19-4726-b25f-09465eea8336
    status: accepted
    candidate_group_id: d439e3f0-eafd-4b71-a843-e881f89e04eb
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/**
---

# Core Module Architecture for Validation Engine and Global Registry Management: Compatibility Adapters External Schema Converters Delegate

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CORE-001** SHOULD: Compatibility adapters and external schema converters SHOULD delegate directly to core registry lookups and standard schema protocols to preserve uniform parsing semantics.
- **R-CORE-002** MANDATORY: Organize internal imports so that dependent compatibility and transformation layers access core modules via relative boundary entry points without circumventing internal directory scoping.
- **R-CORE-003** MANDATORY: When extending schema parsing behavior, implement custom validation logic as discrete check primitives within the core layer before registering public schema methods.

### Verify

```bash
# Discover and run the project static analysis and linting command to verify module boundary compliance.
# Discover and execute the project test runner across core module test suites.
# Discover and execute the circular dependency checker script defined in the project configuration.
```

**Accept when:**
- All core module test suites complete with zero errors.
- Static dependency validation passes without detecting disallowed inward imports into the core module layer.
- Schema registry resolution tests verify deterministic cache lookups across compatibility facades.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated dependency graph validation, static lint checks, and peer code reviews are mandatory.
</enforcement>