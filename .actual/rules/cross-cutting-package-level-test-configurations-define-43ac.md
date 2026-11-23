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

These rules are ALWAYS ACTIVE for:
- Unit test suite configuration across all workspace packages
- Global test runner harness setup scripts and lifecycle hooks

### Rules

- **R-TS-001** MUST: Package-level test configurations MUST define subproject options using defineProject and compose them with shared base configurations using mergeConfig.

### Verify

- Discover the root test execution script from the project manifest and execute it to verify workspace test suites run cleanly.
- Discover package manifest test scripts and execute package-level test suites to confirm project configuration inheritance resolves properly.

**Accept when:**

- All package unit test suites execute and pass without configuration resolution errors.
- Configuration merging via mergeConfig resolves without conflicting property overrides or runtime schema warnings.
- Global test lifecycle hooks execute during suite setup and teardown as defined.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline executing unit test suites across all packages.
- Verified by: Code review checks validating that package test configurations use mergeConfig with base configuration imports.
- Violation handling: Pull requests with failing test suites or invalid test configuration resolution are blocked from merging.
- Violation handling: Test configurations that duplicate base settings instead of using inheritance must be refactored before approval.
- Exception process: Teams requiring divergent test runner configurations must submit an architectural review request explaining why base configuration inheritance cannot be used.
</enforcement>
