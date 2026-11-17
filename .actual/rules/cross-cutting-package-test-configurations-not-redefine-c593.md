---
version: 2
name: cross-cutting-package-test-configurations-not-redefine-c593
description: "Workspace Test Configuration Inheritance via vitest/config defineProject and mergeConfig: Package Test Configurations Not Redefine Base"
metadata:
  actual:
    adr_id: c593601b-b4c1-4218-bb1f-7eebef0a8cfa
    status: accepted
    candidate_group_id: 6efc0e41-02f6-440a-904f-b0bdbf205aab
    evidence:
      source: deep
  scope:
    root: packages/mini
---

# Workspace Test Configuration Inheritance via vitest/config defineProject and mergeConfig: Package Test Configurations Not Redefine Base

Scope: applies to `packages/mini/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-TEST-001** MUST_NOT: Package test configurations MUST NOT redefine base runner capabilities or core execution plugins that are already standardized at the repository level.

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