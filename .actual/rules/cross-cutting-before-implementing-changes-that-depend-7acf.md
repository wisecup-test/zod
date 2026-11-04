---
version: 2
name: cross-cutting-before-implementing-changes-that-depend-7acf
description: "standard-schema Module Adoption: Before Implementing Changes That Depend External"
metadata:
  actual:
    adr_id: 7acfd961-d79e-4e54-944a-9dcac308f932
    status: accepted
    candidate_group_id: cde02561-665e-40aa-bc54-b52077956cb9
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# standard-schema Module Adoption: Before Implementing Changes That Depend External

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-SSM-001** MUST: Before implementing changes that depend on external or shared specification packages, the consumer MUST discover the repository lock artifact and verify the exact resolved version and specification compliance.

### Verify

```bash
# Discover the repository build and test script in the project manifest and execute the core test suite to verify contract compliance.
# Discover the repository linter and type-checker commands from project configuration and verify zero contract violations across core modules.
```

**Accept when:**
- All core schema transformations and error definitions pass automated type-checking and unit test suites verifying conformity to the standard-schema module contracts.
- Dependency analysis confirms no cyclic dependencies or direct bypasses of the standard-schema module in core schema transformation modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull request builds fail if circular imports or standard-schema contract bypasses are introduced.
</enforcement>