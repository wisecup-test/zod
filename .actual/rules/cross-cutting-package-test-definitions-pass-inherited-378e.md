---
version: 2
name: cross-cutting-package-test-definitions-pass-inherited-378e
description: "Workspace Test Configuration Inheritance via vitest/config defineProject and mergeConfig: Package Test Definitions Pass Inherited Base"
metadata:
  actual:
    adr_id: 378eb2f6-1bc7-475f-91e5-cf1e765a5d82
    status: accepted
    candidate_group_id: 6efc0e41-02f6-440a-904f-b0bdbf205aab
    evidence:
      source: deep
  scope:
    root: packages/mini
---

# Workspace Test Configuration Inheritance via vitest/config defineProject and mergeConfig: Package Test Definitions Pass Inherited Base

Scope: applies to `packages/mini/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-TEST-001** MUST: Package test definitions MUST pass the inherited base configuration into mergeConfig alongside package-specific settings to preserve repository-wide test defaults.

### Verify

```bash
# Discover and execute the project test runner script across all workspace packages to verify test configuration resolution.
# Discover and run the project static analysis or linting command to ensure compliance with test configuration import standards.
```

**Accept when:**
- Workspace test configuration files successfully import defineProject and mergeConfig from vitest/config to extend the base configuration.
- The repository verification suite executes all workspace unit tests without configuration resolution errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>