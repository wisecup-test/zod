---
version: 2
name: cross-cutting-before-implementing-updating-test-config-db43
description: "Vitest Project Configuration via defineProject and mergeConfig: Before Implementing Updating Test Configurations That"
metadata:
  actual:
    adr_id: db433440-4b73-45e5-9212-5ea528ba6357
    status: accepted
    candidate_group_id: 3df92587-e67c-4c97-9ee1-b9c7703662f4
    evidence:
      source: deep
  scope:
    root: packages/docs
---

# Vitest Project Configuration via defineProject and mergeConfig: Before Implementing Updating Test Configurations That

Scope: applies to `packages/docs/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-VIT-001** MUST: Before implementing or updating test configurations that depend on vitest/config, the consumer MUST discover the project dependency manifest and authoritative resolution lock artifact to resolve the exact installed dependency version and verify API compatibility against official version reference documentation.

### Verify

```bash
# Discover the repository test execution script from the workspace root manifest and execute the workspace-wide test suite
# Discover the repository configuration linting script from the workspace root manifest and execute it
# (Commands must be derived from project repository manifests per DISCOVERY POLICY)
```

**Accept when:**
- All sub-package test configurations successfully merge the shared root configuration without schema validation errors during test initialization.
- The workspace test runner discovers and executes tests across all configured sub-projects with unified reporting output.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>