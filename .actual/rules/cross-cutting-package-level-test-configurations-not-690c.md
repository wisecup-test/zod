---
version: 2
name: cross-cutting-package-level-test-configurations-not-690c
description: "Vitest Configuration Composition for Unit Testing: Package Level Test Configurations Not Redeclare"
metadata:
  actual:
    adr_id: 690c0ebb-b606-47a4-a188-7e3f789ef349
    status: accepted
    candidate_group_id: baa2b941-9eff-40d1-af1e-1b8fcd3b43b1
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/docs/**
      - packages/resolution/**
      - packages/zod/**
      - scripts/**
      - vitest.config.ts
---

# Vitest Configuration Composition for Unit Testing: Package Level Test Configurations Not Redeclare

Scope: applies to `packages/docs/**`, `packages/resolution/**`, `packages/zod/**`, `scripts/**`, `vitest.config.ts`.

These rules are ALWAYS ACTIVE for all unit test suite configurations across workspace packages and global test runner harness setup scripts.

### Rules

- **R-VIT-001** MUST_NOT: Package-level test configurations MUST NOT redeclare shared runner options independently when base configuration inheritance is supported.

### Verify

```bash
# Discover and run workspace-level test execution
# (Discover test command from project manifest and execute)

# Discover and run package-level test suites to verify configuration inheritance
# (Discover package manifests and execute tests)
```

**Accept when:**
- All package unit test suites execute and pass without configuration resolution errors.
- Configuration merging resolves without conflicting property overrides or runtime schema warnings.
- Global test lifecycle hooks execute during suite setup and teardown as defined.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>