---
version: 2
name: cross-cutting-consumers-discover-project-dependency-lo-2ce5
description: "Vitest Configuration Composition for Unit Testing: Consumers Discover Project Dependency Lock Artifact"
metadata:
  actual:
    adr_id: 2ce54b27-9b4b-4800-a4a4-cbd150f257f1
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

# Vitest Configuration Composition for Unit Testing: Consumers Discover Project Dependency Lock Artifact

Scope: applies to `packages/docs/**`, `packages/resolution/**`, `packages/zod/**`, `scripts/**`, `vitest.config.ts`.

These rules are ALWAYS ACTIVE for unit test suite configuration across all workspace packages and global test runner harness setup scripts and lifecycle hooks.

### Rules

- **R-VIT-001** MUST: Consumers MUST discover the project dependency lock artifact and verify the exact resolved version of Vitest before authoring or modifying test configuration files.

### Verify

```bash
# Discover and execute the root test execution script from the project manifest
root_test_script=$(node -p "require('./package.json').scripts['test']")
if [ -n "$root_test_script" ]; then
  npm run test
fi
```

**Accept when:**
- All package unit test suites execute and pass without configuration resolution errors.
- Configuration merging via mergeConfig resolves without conflicting property overrides or runtime schema warnings.
- Global test lifecycle hooks execute during suite setup and teardown as defined.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>