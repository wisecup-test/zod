---
version: 2
name: cross-cutting-before-implementing-updating-test-projec-102a
description: "Package Test Project Configuration Composition via vitest/config: Before Implementing Updating Test Project Configurations"
metadata:
  actual:
    adr_id: 102a5c05-b36c-482f-91f4-8b10edbdddcd
    status: accepted
    candidate_group_id: 682b8cfd-bb53-4c8c-8bb2-12185574b204
    evidence:
      source: deep
  scope:
    root: packages/zod
---

# Package Test Project Configuration Composition via vitest/config: Before Implementing Updating Test Project Configurations

Scope: applies to `packages/zod/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-VITEST-001** MUST: Before implementing or updating test project configurations, consumers MUST inspect the repository lock artifact to determine the exact resolved version of vitest/config and verify API compatibility against official documentation.

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