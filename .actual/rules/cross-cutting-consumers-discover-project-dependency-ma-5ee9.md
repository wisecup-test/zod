---
version: 2
name: cross-cutting-consumers-discover-project-dependency-ma-5ee9
description: "Internal Core Module Integration for Localization Modules: Consumers Discover Project Dependency Manifest Authoritative"
metadata:
  actual:
    adr_id: 5ee962d4-ed29-4a11-9ac0-70c58df6d229
    status: accepted
    candidate_group_id: a9c62ae4-f0d0-459b-84d7-cef8e7278899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/locales/**
---

# Internal Core Module Integration for Localization Modules: Consumers Discover Project Dependency Manifest Authoritative

Scope: applies to `packages/zod/src/v4/locales/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-COR-001** MUST: Consumers MUST discover the project dependency manifest and authoritative lock artifact to verify exact dependency resolutions prior to modifying or implementing module integrations.

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