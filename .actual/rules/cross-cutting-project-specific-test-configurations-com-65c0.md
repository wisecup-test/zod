---
version: 2
name: cross-cutting-project-specific-test-configurations-com-65c0
description: "Vitest Project Configuration via defineProject and mergeConfig: Project Specific Test Configurations Compose Their"
metadata:
  actual:
    adr_id: 65c0f7a4-c8ca-45f8-a108-4418bcb69f1d
    status: accepted
    candidate_group_id: 3df92587-e67c-4c97-9ee1-b9c7703662f4
    evidence:
      source: deep
  scope:
    root: packages/docs
---

# Vitest Project Configuration via defineProject and mergeConfig: Project Specific Test Configurations Compose Their

Scope: applies to `packages/docs/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-VITEST-001** MUST: Project-specific test configurations MUST compose their settings with the shared root test configuration using mergeConfig from vitest/config rather than redefining global execution parameters independently.

### Verify

```bash
# Discover the repository test execution script from the workspace root manifest and execute the workspace-wide test suite
# Discover the repository configuration linting script from the workspace root manifest and execute it
```

**Accept when:**
- All sub-package test configurations successfully merge the shared root configuration without schema validation errors during test initialization.
- The workspace test runner discovers and executes tests across all configured sub-projects with unified reporting output.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>