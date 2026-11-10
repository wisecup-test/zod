---
version: 2
name: cross-cutting-cross-cutting-schema-metadata-instance-8f5a
description: "Core Module Architecture for Validation Engine and Global Registry Management: Cross Cutting Schema Metadata Instance Tracking"
metadata:
  actual:
    adr_id: 8f5a48f3-122b-4ff0-a099-da787d167304
    status: accepted
    candidate_group_id: d439e3f0-eafd-4b71-a843-e881f89e04eb
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/**
---

# Core Module Architecture for Validation Engine and Global Registry Management: Cross Cutting Schema Metadata Instance Tracking

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for implementation and extension of validation schemas, checks, and error structures, registration and resolution of schema metadata within internal registries, and integration of schema transformation processors and legacy compatibility adapters.

### Rules

- **R-CORE-001** MUST: Cross-cutting schema metadata and instance tracking MUST interact through the global registry interface rather than maintaining localized state within validation schemas.

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
Claude Code MUST NOT skip or defer verification. Automated dependency graph validation, static lint checks, and peer code reviews are mandatory for any changes altering core module interfaces or registry structures.
</enforcement>