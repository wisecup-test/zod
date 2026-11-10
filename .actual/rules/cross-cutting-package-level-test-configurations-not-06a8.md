---
version: 2
name: cross-cutting-package-level-test-configurations-not-06a8
description: "Vitest Project Configuration via defineProject and mergeConfig: Package Level Test Configurations Not Override"
metadata:
  actual:
    adr_id: 06a848f9-7ce4-484c-8caf-c18d2857510f
    status: accepted
    candidate_group_id: 3df92587-e67c-4c97-9ee1-b9c7703662f4
    evidence:
      source: deep
  scope:
    root: packages/docs
---

# Vitest Project Configuration via defineProject and mergeConfig: Package Level Test Configurations Not Override

Scope: applies to `packages/docs/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-VITEST-001** MUST_NOT: Package-level test configurations MUST NOT override shared root test orchestration settings, global coverage thresholds, or shared reporter definitions unless an explicit package exception is documented.

### Verify

```bash
# Discover the repository test execution script from the workspace root manifest and execute the workspace-wide test suite
# Discover the repository configuration linting script from the workspace root manifest and execute it
```

**Accept when:**
- All sub-package test configurations successfully merge the shared root configuration without schema validation errors during test initialization.
- The workspace test runner discovers and executes tests across all configured sub-projects with unified reporting output.

<enforcement>
Claude Code MUST NOT skip or defer verification. All sub-package test configuration modifications must be verified via automated test execution and linting scripts.
</enforcement>