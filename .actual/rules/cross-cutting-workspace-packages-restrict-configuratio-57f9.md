---
version: 2
name: cross-cutting-workspace-packages-restrict-configuratio-57f9
description: "Workspace Test Configuration Inheritance via vitest/config defineProject and mergeConfig: Workspace Packages Restrict Configuration Overrides Package"
metadata:
  actual:
    adr_id: 57f95897-8002-47b0-ad36-c96e2404bc69
    status: accepted
    candidate_group_id: 6efc0e41-02f6-440a-904f-b0bdbf205aab
    evidence:
      source: deep
  scope:
    root: packages/mini
---

# Workspace Test Configuration Inheritance via vitest/config defineProject and mergeConfig: Workspace Packages Restrict Configuration Overrides Package

Scope: applies to `packages/mini/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-WTC-001** SHOULD: Workspace packages SHOULD restrict configuration overrides to package-specific source boundaries, unique environment flags, and local test setup hooks.

### Verify

```bash
# Discover and execute the project test runner script across all workspace packages to verify test configuration resolution
# Discover and run the project static analysis or linting command to ensure compliance with test configuration import standards
```

**Accept when:**
- Workspace test configuration files successfully import defineProject and mergeConfig from vitest/config to extend the base configuration.
- The repository verification suite executes all workspace unit tests without configuration resolution errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>