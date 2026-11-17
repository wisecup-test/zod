---
version: 2
name: cross-cutting-before-implementing-updating-modules-tha-a492
description: "Standard Schema Interface Adoption: Before Implementing Updating Modules That Rely"
metadata:
  actual:
    adr_id: a492b51f-54e4-432c-8022-1a1002c4f65e
    status: accepted
    candidate_group_id: 1044d40f-34d5-44f9-a360-a138cf5e1eb0
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Standard Schema Interface Adoption: Before Implementing Updating Modules That Rely

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for core schema definition modules, validation engines, error normalization pipelines, serialization adapters, and schema introspection utilities.

### Rules

- **R-SSIA-001** MUST: Before implementing or updating modules that rely on the Standard Schema specification, consumers MUST inspect the repository dependency lock artifact to determine the exact resolved specification version and verify contract compatibility.
- **R-SSIA-002** MUST (DISCOVERY POLICY): The consumer MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-SSIA-003** MUST (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: find the dependency manifest, identify the build tool, inspect the lock/resolution artifact for the exact resolved version, look up official documentation for that exact version, confirm every API exists, and re-run steps per dependency at point of use.
- **R-SSIA-004** SHOULD: Inspect the repository dependency graph to identify existing schema metadata registries and caching layers before implementing new transformation adapters.
- **R-SSIA-005** MUST: Ensure all schema traversal procedures incorporate cache lookups and prototype safety guards to handle recursive definitions safely.

### Verify

```bash
# Discover and execute the project repository static type verification suite to confirm interface conformance across all core modules.
# Execute the project automated test suite to ensure schema transformation and error reporting behavior complies with specification contracts.
```

**Accept when:**
- All core schema compilation, error handling, and serialization modules pass static type verification without interface mismatches.
- Automated unit and integration test suites succeed with zero regressions in schema validation or issue formatting.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration pipelines, static type analysis, and automated test suites verify compliance. Contributions introducing proprietary validation interfaces or non-compliant issue structures are rejected.
</enforcement>