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

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-VIT-001** MUST: Teams MUST use Vitest configuration composition functions defineConfig, defineProject, and mergeConfig from vitest/config to define and inherit workspace unit testing configurations.

### Verify

```bash
# Discover the root test execution script from the project manifest and execute it
root_script=$(node -p "require('./package.json').scripts['test'] || ''")
if [ -n "$root_script" ]; then
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