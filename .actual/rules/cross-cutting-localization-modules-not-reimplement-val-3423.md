---
version: 2
name: cross-cutting-localization-modules-not-reimplement-val-3423
description: "Internal Core Module Integration for Localization Modules: Localization Modules Not Reimplement Validation Checks"
metadata:
  actual:
    adr_id: 3423f9cc-a00a-42af-85d1-ca3c8ec8186d
    status: accepted
    candidate_group_id: a9c62ae4-f0d0-459b-84d7-cef8e7278899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/locales/**
---

# Internal Core Module Integration for Localization Modules: Localization Modules Not Reimplement Validation Checks

Scope: applies to `packages/zod/src/v4/locales/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-LOC-001** MUST_NOT: Localization modules MUST NOT reimplement validation checks, error categorization, or formatting utility logic independently within individual locale definitions.

### Verify

```bash
# Discover and run project static analysis, linting scripts, and test suites to verify module import constraints and localization error formatting against core check specifications.
# (Exact commands must be discovered from the project repository configuration)
```

**Accept when:**
- All localization modules successfully import core checks, errors, and utilities without boundary violations.
- Test suites pass for all locale modules with consistent error formatting behavior.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests with non-compliant imports or duplicated core logic are blocked from merging.
</enforcement>