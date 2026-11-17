---
version: 2
name: cross-cutting-before-implementing-modifying-test-confi-576e
description: "Workspace Test Configuration Inheritance via vitest/config defineProject and mergeConfig: Before Implementing Modifying Test Configurations That"
metadata:
  actual:
    adr_id: 576e76e2-cc95-432f-aa47-9660488cc8b6
    status: accepted
    candidate_group_id: 6efc0e41-02f6-440a-904f-b0bdbf205aab
    evidence:
      source: deep
  scope:
    root: packages/mini
---

# Workspace Test Configuration Inheritance via vitest/config defineProject and mergeConfig: Before Implementing Modifying Test Configurations That

Scope: applies to `packages/mini/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-TEST-001** MUST: Before implementing or modifying test configurations that depend on the test framework configuration module, the consumer MUST inspect the repository lock artifact to determine the exact resolved version and verify API compatibility.

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