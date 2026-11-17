---
version: 2
name: cross-cutting-package-test-configurations-scope-config-6b1a
description: "Package Test Project Configuration Composition via vitest/config: Package Test Configurations Scope Configuration Properties"
metadata:
  actual:
    adr_id: 6b1a4381-ed08-4a5b-9007-6673d12d77af
    status: accepted
    candidate_group_id: 682b8cfd-bb53-4c8c-8bb2-12185574b204
    evidence:
      source: deep
  scope:
    root: packages/zod
---

# Package Test Project Configuration Composition via vitest/config: Package Test Configurations Scope Configuration Properties

Scope: applies to `packages/zod/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-PTCC-001** SHOULD: Package test configurations SHOULD scope configuration properties strictly to package-specific source boundaries and test environment requirements.

### Verify

```bash
find . -maxdepth 3 -type f -exec grep -l "defineProject" {} +
find . -maxdepth 3 -type f -exec grep -l "mergeConfig" {} +
REPO_ROOT=$(git rev-parse --show-toplevel 2>/dev/null || pwd) && grep -rn "from [\"']vitest/config[\"']" "$REPO_ROOT"
```

**Accept when:**
- Package test configuration modules import defineProject and mergeConfig from vitest/config.
- Package test project definitions compose the shared root configuration with package-specific overrides via mergeConfig.
- Project test verification directives execute package test suites without configuration composition errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>