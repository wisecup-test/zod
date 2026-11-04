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

These rules are ALWAYS ACTIVE for all unit test suite configurations and global test runner harness setups across all workspace packages.

### Rules

- **R-VIT-001** MUST: Global test environment lifecycle assertions and fixtures MUST use beforeAll and afterAll hooks imported directly from vitest.
- **R-VIT-002** MUST: Global test runner configurations be defined at the workspace root, exporting defaults that package configurations can import and combine using mergeConfig.
- **R-VIT-003** MUST: Use defineProject within package directories to scope test execution targets and environment variables specifically for that package unit tests.
- **R-VIT-004** MANDATORY: The consumer MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-VIT-005** MANDATORY: Before writing code that uses a versioned library, execute the lock-version grounding process: find the dependency manifest, identify the build tool, inspect the resolution artifact for the exact version, look up official documentation for that exact version, and confirm every API/class/function exists in that version.

### Verify

```bash
# Discover and execute the root test execution script from the project manifest
# Discover and execute package manifest test scripts to confirm configuration inheritance
# Run the project test suite using the detected test command
npm test
```

**Accept when:**
- All package unit test suites execute and pass without configuration resolution errors.
- Configuration merging via mergeConfig resolves without conflicting property overrides or runtime schema warnings.
- Global test lifecycle hooks execute during suite setup and teardown as defined.

<enforcement>
Verification is mandatory. Claude Code MUST NOT skip or defer verification of unit test suites, configuration merging, or lifecycle hooks.
</enforcement>