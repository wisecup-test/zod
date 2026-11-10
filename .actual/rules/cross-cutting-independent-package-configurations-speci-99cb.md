---
version: 2
name: cross-cutting-independent-package-configurations-speci-99cb
description: "Vitest Project Configuration via defineProject and mergeConfig: Independent Package Configurations Specify Custom Test"
metadata:
  actual:
    adr_id: 99cb1354-e6cb-43d1-a91d-fc217a1cff10
    status: accepted
    candidate_group_id: 3df92587-e67c-4c97-9ee1-b9c7703662f4
    evidence:
      source: deep
  scope:
    root: packages/docs
---

# Vitest Project Configuration via defineProject and mergeConfig: Independent Package Configurations Specify Custom Test

Scope: applies to `packages/docs/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-VITEST-001** MAY: Independent package configurations MAY specify custom test timeout thresholds or execution pool constraints when workload characteristics require package-specific runtime isolation.

### Verify

```bash
# Discover the repository test execution script from the workspace root manifest and execute the workspace-wide test suite to confirm all project configurations resolve and pass.
# Discover the repository configuration linting script from the workspace root manifest and execute it to verify conformance of all sub-project test configuration files.
```

**Accept when:**
- All sub-package test configurations successfully merge the shared root configuration without schema validation errors during test initialization.
- The workspace test runner discovers and executes tests across all configured sub-projects with unified reporting output.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>