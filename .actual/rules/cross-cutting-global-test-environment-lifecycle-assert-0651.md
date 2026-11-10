---
version: 2
name: cross-cutting-global-test-environment-lifecycle-assert-0651
description: "Vitest Configuration Composition for Unit Testing: Global Test Environment Lifecycle Assertions Fixtures"
metadata:
  actual:
    adr_id: 06516c3a-7668-4b7d-93dd-bb6446212980
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

# Vitest Configuration Composition for Unit Testing: Global Test Environment Lifecycle Assertions Fixtures

Scope: applies to `packages/docs/**`, `packages/resolution/**`, `packages/zod/**`, `scripts/**`, `vitest.config.ts`.

These rules are ALWAYS ACTIVE for unit test suite configuration across all workspace packages and global test runner harness setup scripts and lifecycle hooks.

### Rules

- **R-VITEST-001** MUST: Global test environment lifecycle assertions and fixtures MUST use beforeAll and afterAll hooks imported directly from vitest.

### Verify

```bash
# Discover and execute the root test execution script from the project manifest
root_test_script=$(node -p "require('./package.json').scripts['test']")
npm run test

# Discover and execute package-level test suites to confirm configuration inheritance
for pkg in packages/*; do
  if [ -f "$pkg/package.json" ]; then
    npm --prefix "$pkg" test --if-present
  fi
done
```

**Accept when:**
- All package unit test suites execute and pass without configuration resolution errors.
- Configuration merging via mergeConfig resolves without conflicting property overrides or runtime schema warnings.
- Global test lifecycle hooks execute during suite setup and teardown as defined.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>