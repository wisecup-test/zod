---
version: 2
name: cross-cutting-localization-modules-import-consume-vali-1d2f
description: "Internal Core Module Integration for Localization Modules: Localization Modules Import Consume Validation Checks"
metadata:
  actual:
    adr_id: 1d2f6bf1-8b29-45f9-a67d-dd1fce667646
    status: accepted
    candidate_group_id: a9c62ae4-f0d0-459b-84d7-cef8e7278899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/locales/**
---

# Internal Core Module Integration for Localization Modules: Localization Modules Import Consume Validation Checks

Scope: applies to `packages/zod/src/v4/locales/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-LOC-001** MUST: Localization modules MUST import and consume validation checks, error definitions, and utility helpers exclusively from the shared internal core module.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify module import constraints across localization modules.
# Discover and execute the repository test suite to validate locale error formatting against core check specifications.
```

**Accept when:**
- All localization modules successfully import core checks, errors, and utilities without boundary violations.
- Test suites pass for all locale modules with consistent error formatting behavior.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>