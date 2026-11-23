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

These rules are ALWAYS ACTIVE for:
- Unit and integration test configuration across individual workspace packages.
- Sub-project test definitions inheriting from shared repository-level test configurations.

### Rules

- **R-TS-001** MUST: Packages defining localized test execution suites MUST declare project-level configuration using defineProject imported from vitest/config.

### Verify

- Discover the repository test execution script from the workspace root manifest and execute the workspace-wide test suite to confirm all project configurations resolve and pass.
- Discover the repository configuration linting script from the workspace root manifest and execute it to verify conformance of all sub-project test configuration files.

**Accept when:**

- All sub-package test configurations successfully merge the shared root configuration without schema validation errors during test initialization.
- The workspace test runner discovers and executes tests across all configured sub-projects with unified reporting output.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline execution verifying project test configuration resolution.
- Verified by: Peer code review for all modifications to sub-package test configuration files.
- Violation handling: Pull requests containing unmerged, duplicate standalone configurations without documented approval are blocked from merging.
- Violation handling: Static analysis warnings or build failures triggered by invalid project configuration schemas.
- Exception process: Submit an architectural review request outlining package-specific technical constraints that necessitate divergence from root test configuration.
</enforcement>
