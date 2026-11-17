---
version: 2
name: cross-cutting-core-modules-not-bypass-standard-00a7
description: "Standard Schema Interface Adoption: Core Modules Not Bypass Standard Schema"
metadata:
  actual:
    adr_id: 00a74422-e978-4e81-a445-d431d06bfa18
    status: accepted
    candidate_group_id: 1044d40f-34d5-44f9-a360-a138cf5e1eb0
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Standard Schema Interface Adoption: Core Modules Not Bypass Standard Schema

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema definition modules, validation engines, error normalization pipelines, serialization adapters, and schema introspection utilities.

### Rules

- **R-SSIA-001** MUST_NOT: Core modules MUST NOT bypass Standard Schema contracts when exposing schema inspection or metadata access to external consumers or serialization adapters.

### Verify

```bash
# Discover and execute the project repository static type verification suite to confirm interface conformance across all core modules.
# Execute the project automated test suite to ensure schema transformation and error reporting behavior complies with specification contracts.
```

**Accept when:**
- All core schema compilation, error handling, and serialization modules pass static type verification without interface mismatches.
- Automated unit and integration test suites succeed with zero regressions in schema validation or issue formatting.

<enforcement>
Claude Code MUST NOT skip or defer verification. All code contributions are verified via continuous integration pipelines executing static type analysis, automated test suites, and peer architectural reviews.
</enforcement>