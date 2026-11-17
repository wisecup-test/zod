---
version: 2
name: cross-cutting-packages-defining-localized-test-executi-b443
description: "Vitest Project Configuration via defineProject and mergeConfig: Packages Defining Localized Test Execution Suites"
metadata:
  actual:
    adr_id: b443d710-e906-4bec-b7e4-acb67f15ed9c
    status: accepted
    candidate_group_id: 3df92587-e67c-4c97-9ee1-b9c7703662f4
    evidence:
      source: deep
  scope:
    root: packages/docs
---

# Vitest Project Configuration via defineProject and mergeConfig: Packages Defining Localized Test Execution Suites

Scope: applies to `packages/docs/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-VITEST-001** MUST: Packages defining localized test execution suites MUST declare project-level configuration using defineProject imported from vitest/config.

### Verify

```bash
# Discover the repository test execution script from the workspace root manifest and execute
# the workspace-wide test suite to confirm all project configurations resolve and pass.
# (Tool names, commands, and package managers must be discovered from the repository per discovery policy)
```

**Accept when:**
- All sub-package test configurations successfully merge the shared root configuration without schema validation errors during test initialization.
- The workspace test runner discovers and executes tests across all configured sub-projects with unified reporting output.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>