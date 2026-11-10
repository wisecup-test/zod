---
version: 2
name: cross-cutting-error-reporting-routines-normalize-valid-ac60
description: "Standard Schema Interface Adoption: Error Reporting Routines Normalize Validation Failures"
metadata:
  actual:
    adr_id: ac6019f8-5695-46e8-8039-20e6332461f1
    status: accepted
    candidate_group_id: 1044d40f-34d5-44f9-a360-a138cf5e1eb0
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Standard Schema Interface Adoption: Error Reporting Routines Normalize Validation Failures

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema definition modules, validation engines, error normalization pipelines, and serialization adapters translating validation definitions.

### Rules

- **R-SS-001** SHOULD: Error reporting routines SHOULD normalize validation failures through the standardized issue structure defined by the Standard Schema specification rather than generating proprietary error trees.
- **R-SS-002** MANDATORY: Developers MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-SS-003** MANDATORY: Before writing code that uses a versioned library, developers MUST execute the lock-version grounding sequence (discover dependency manifest, identify build tool, inspect repository lock/resolution artifact for the exact resolved version, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-verify per dependency at point of use).
- **R-SS-004** MANDATORY: Inspect the repository dependency graph to identify existing schema metadata registries and caching layers before implementing new transformation adapters.
- **R-SS-005** MANDATORY: Ensure all schema traversal procedures incorporate cache lookups and prototype safety guards to handle recursive definitions safely.

### Verify

```bash
# Discover and execute the project repository static type verification suite to confirm interface conformance across all core modules.
# Execute the project automated test suite to ensure schema transformation and error reporting behavior complies with specification contracts.
```

**Accept when:**
- All core schema compilation, error handling, and serialization modules pass static type verification without interface mismatches.
- Automated unit and integration test suites succeed with zero regressions in schema validation or issue formatting.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by continuous integration pipelines executing static type analysis and automated test suites, and peer architectural reviews verifying contract compliance against the Standard Schema specification.
</enforcement>