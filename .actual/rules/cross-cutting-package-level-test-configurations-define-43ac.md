---
version: 2
name: cross-cutting-package-level-test-configurations-define-43ac
description: "Vitest Configuration Composition for Unit Testing: Package Level Test Configurations Define Subproject"
metadata:
  actual:
    adr_id: 43ac1da7-ecaa-483b-b31e-719d73ad971a
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

# Vitest Configuration Composition for Unit Testing: Package Level Test Configurations Define Subproject

Scope: applies to `packages/docs/**`, `packages/resolution/**`, `packages/zod/**`, `scripts/**`, `vitest.config.ts`.

These rules are ALWAYS ACTIVE for all unit test suite configurations across workspace packages and global test runner harness setup scripts and lifecycle hooks.

### Rules

- **R-VIT-001** MUST: Package-level test configurations MUST define subproject options using defineProject and compose them with shared base configurations using mergeConfig.

### Verify

```bash
# Discover the root test execution script from the project manifest and execute it to verify workspace test suites run cleanly.
# Discover package manifest test scripts and execute package-level test suites to confirm project configuration inheritance resolves properly.
```

**Accept when:**
- All package unit test suites execute and pass without configuration resolution errors.
- Configuration merging via mergeConfig resolves without conflicting property overrides or runtime schema warnings.
- Global test lifecycle hooks execute during suite setup and teardown as defined.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>