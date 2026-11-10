---
version: 2
name: cross-cutting-package-configurations-restrict-localize-df1b
description: "Vitest Project Configuration via defineProject and mergeConfig: Package Configurations Restrict Localized Customizations Strictly"
metadata:
  actual:
    adr_id: df1b0e0f-9906-4566-987e-987665a58c62
    status: accepted
    candidate_group_id: 3df92587-e67c-4c97-9ee1-b9c7703662f4
    evidence:
      source: deep
  scope:
    root: packages/docs
---

# Vitest Project Configuration via defineProject and mergeConfig: Package Configurations Restrict Localized Customizations Strictly

Scope: applies to `packages/docs/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ADR-001** SHOULD: Package configurations SHOULD restrict localized customizations strictly to package-specific environment variables, setup files, and test pattern matchers.

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