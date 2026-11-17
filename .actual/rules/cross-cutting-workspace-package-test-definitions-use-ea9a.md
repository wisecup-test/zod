---
version: 2
name: cross-cutting-workspace-package-test-definitions-use-ea9a
description: "Workspace Test Configuration Inheritance via vitest/config defineProject and mergeConfig: Workspace Package Test Definitions Use Defineproject"
metadata:
  actual:
    adr_id: ea9a78c3-74a0-4f56-98fe-0349db29022e
    status: accepted
    candidate_group_id: 6efc0e41-02f6-440a-904f-b0bdbf205aab
    evidence:
      source: deep
  scope:
    root: packages/mini
---

# Workspace Test Configuration Inheritance via vitest/config defineProject and mergeConfig: Workspace Package Test Definitions Use Defineproject

Scope: applies to `packages/mini/**`.

These rules are ALWAYS ACTIVE for all unit test configuration files located within workspace packages.

### Rules

- **R-WSP-001** MUST: Workspace package test definitions MUST use defineProject and mergeConfig from vitest/config to extend the shared base test configuration.

### Verify

```bash
# Discover and execute the project test runner script across all workspace packages
# Example: pnpm test --run
# Discover and run static analysis or linting to check import standards
```

**Accept when:**
- Workspace test configuration files successfully import defineProject and mergeConfig from vitest/config to extend the base configuration.
- The repository verification suite executes all workspace unit tests without configuration resolution errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>