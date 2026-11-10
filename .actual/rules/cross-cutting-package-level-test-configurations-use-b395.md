---
version: 2
name: cross-cutting-package-level-test-configurations-use-b395
description: "Package Test Project Configuration Composition via vitest/config: Package Level Test Configurations Use Mergeconfig"
metadata:
  actual:
    adr_id: b3956f8b-a717-489b-9e03-98fcd76c8fcf
    status: accepted
    candidate_group_id: 682b8cfd-bb53-4c8c-8bb2-12185574b204
    evidence:
      source: deep
  scope:
    root: packages/zod
---

# Package Test Project Configuration Composition via vitest/config: Package Level Test Configurations Use Mergeconfig

Scope: applies to `packages/zod/**`.

These rules are ALWAYS ACTIVE for workspace packages requiring package-specific unit testing configurations within a multi-package repository.

### Rules

- **R-VITEST-001** MUST: Package-level test configurations MUST use mergeConfig from vitest/config to compose package-specific overrides with the shared root configuration rather than duplicating baseline settings.

### Verify

```bash
find . -maxdepth 3 -type f -exec grep -l "defineProject" {} +
find . -maxdepth 3 -type f -exec grep -l "mergeConfig" {} +
REPO_ROOT=$(git rev-parse --show-toplevel 2>/dev/null || pwd) && grep -rn "from \["'"]vitest/config\["'"]" "$REPO_ROOT"
```

**Accept when:**
- Package test configuration modules import defineProject and mergeConfig from vitest/config.
- Package test project definitions compose the shared root configuration with package-specific overrides via mergeConfig.
- Project test verification directives execute package test suites without configuration composition errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>