---
version: 2
name: cross-cutting-schema-transformation-serialization-adap-b81f
description: "Standard Schema Interface Adoption: Schema Transformation Serialization Adapters Consume Emit"
metadata:
  actual:
    adr_id: b81fe201-2bbe-4884-aea5-7a6ed351e1dd
    status: accepted
    candidate_group_id: 1044d40f-34d5-44f9-a360-a138cf5e1eb0
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Standard Schema Interface Adoption: Schema Transformation Serialization Adapters Consume Emit

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for core schema definition modules, validation engines, error normalization pipelines, serialization adapters, and schema introspection utilities.

### Rules

- **R-SS-001** MUST: Schema transformation and serialization adapters MUST consume and emit validation structures that conform directly to Standard Schema definitions without introducing proprietary intermediate layers.

### Verify

```bash
# Discover and execute the project repository static type verification suite
# Execute the project automated test suite
```

**Accept when:**
- All core schema compilation, error handling, and serialization modules pass static type verification without interface mismatches.
- Automated unit and integration test suites succeed with zero regressions in schema validation or issue formatting.

<enforcement>
Claude Code MUST NOT skip or defer verification. All code contributions must comply with the Standard Schema interface contract.
</enforcement>