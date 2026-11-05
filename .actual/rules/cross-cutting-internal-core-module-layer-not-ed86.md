---
version: 2
name: cross-cutting-internal-core-module-layer-not-ed86
description: "Core Module Architecture for Validation Engine and Global Registry Management: Internal Core Module Layer Not Import"
metadata:
  actual:
    adr_id: ed86b589-db89-4348-9f27-b708c41bfc30
    status: accepted
    candidate_group_id: d439e3f0-eafd-4b71-a843-e881f89e04eb
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/**
---

# Core Module Architecture for Validation Engine and Global Registry Management: Internal Core Module Layer Not Import

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CORE-001** MUST_NOT: The internal core module layer MUST NOT import from outward compatibility facades or high-level schema transformation modules.

### Verify

```bash
# Discover and run the project static analysis and linting command to verify module boundary compliance
# Discover and execute the project test runner across core module test suites
# Discover and execute the circular dependency checker script defined in the project configuration
```

**Accept when:**
- All core module test suites complete with zero errors.
- Static dependency validation passes without detecting disallowed inward imports into the core module layer.
- Schema registry resolution tests verify deterministic cache lookups across compatibility facades.

<enforcement>
Claude Code MUST NOT skip or defer verification. All changes altering core module interfaces or registry structures must pass automated dependency graph validation, static lint checks, and mandatory peer code review.
</enforcement>