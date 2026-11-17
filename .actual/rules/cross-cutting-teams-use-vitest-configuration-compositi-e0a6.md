---
version: 2
name: cross-cutting-teams-use-vitest-configuration-compositi-e0a6
description: "Vitest Configuration Composition for Unit Testing: Teams Use Vitest Configuration Composition Functions"
metadata:
  actual:
    adr_id: e0a695f2-7a66-4c20-bc8b-ae925352bf70
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

# Vitest Configuration Composition for Unit Testing: Teams Use Vitest Configuration Composition Functions

Scope: applies to `packages/docs/**`, `packages/resolution/**`, `packages/zod/**`, `scripts/**`, `vitest.config.ts`.

These rules are ALWAYS ACTIVE for all unit test suite configurations and test runner harness setup scripts across workspace packages.

### Rules

- **R-VIT-001** MUST: Use Vitest configuration composition functions `defineConfig`, `defineProject`, and `mergeConfig` from `vitest/config` to define and inherit workspace unit testing configurations.

### Verify

```bash
# Discover and run the root test execution script from the project manifest
# (e.g., pnpm test, npm test, etc.)
npm test

# Discover and run package-level test scripts to confirm configuration inheritance resolves properly
# (e.g., pnpm --recursive test or running package test scripts individually)
```

**Accept when:**
- All package unit test suites execute and pass without configuration resolution errors.
- Configuration merging via `mergeConfig` resolves without conflicting property overrides or runtime schema warnings.
- Global test lifecycle hooks execute during suite setup and teardown as defined.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipeline executes unit test suites across all packages, and code review checks validate that package test configurations use `mergeConfig` with base configuration imports.
</enforcement>