---
version: 2
name: cross-cutting-error-formatting-validation-issue-builde-e3df
description: "standard-schema Module Adoption: Error Formatting Validation Issue Builders Preserve"
metadata:
  actual:
    adr_id: e3dfcd67-660e-4b39-8d28-fb8cebb9547a
    status: accepted
    candidate_group_id: cde02561-665e-40aa-bc54-b52077956cb9
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# standard-schema Module Adoption: Error Formatting Validation Issue Builders Preserve

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema transformation modules compiling or translating schemas across representation formats, and all core error formatting and validation dispatch utilities requiring standardized schema contracts.

### Rules

- **R-SS-001** SHOULD: Error formatting and validation issue builders SHOULD preserve standard-schema issue structures across serialization boundaries.

### Verify

```bash
# Discover and execute the project build and test script from the project manifest
# Discover and execute the project linter and type-checker commands from project configuration
```

**Accept when:**
- All core schema transformations and error definitions pass automated type-checking and unit test suites verifying conformity to the standard-schema module contracts.
- Dependency analysis confirms no cyclic dependencies or direct bypasses of the standard-schema module in core schema transformation modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>