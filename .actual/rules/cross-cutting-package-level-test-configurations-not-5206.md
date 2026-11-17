---
version: 2
name: cross-cutting-package-level-test-configurations-not-5206
description: "Package Test Project Configuration Composition via vitest/config: Package Level Test Configurations Not Redeclare"
metadata:
  actual:
    adr_id: 52068644-ccb3-408c-811c-60e29952d01d
    status: accepted
    candidate_group_id: 682b8cfd-bb53-4c8c-8bb2-12185574b204
    evidence:
      source: deep
  scope:
    root: packages/zod
---

# Package Test Project Configuration Composition via vitest/config: Package Level Test Configurations Not Redeclare

Scope: applies to `packages/zod/**`.

These rules are ALWAYS ACTIVE for workspace packages requiring package-specific unit testing configurations within a multi-package repository that extend shared workspace baseline settings.

### Rules

- **R-TEST-001** MUST_NOT: Package-level test configurations MUST NOT redeclare global execution defaults, shared reporters, or common coverage thresholds established in the root configuration.

### Verify

```bash
find . -maxdepth 3 -type f -exec grep -l "defineProject" {} +
find . -maxdepth 3 -type f -exec grep -l "mergeConfig" {} +
REPO_ROOT=$(git rev-parse --show-toplevel 2>/dev/null || pwd) && grep -rn "from [\'"]vitest/config[\'"]" "$REPO_ROOT"
```

**Accept when:**
- Package test configuration modules import defineProject and mergeConfig from vitest/config.
- Package test project definitions compose the shared root configuration with package-specific overrides via mergeConfig.
- Project test verification directives execute package test suites without configuration composition errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>