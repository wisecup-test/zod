---
version: 2
name: cross-cutting-modules-adopt-zod-schemas-runtime-fb1f
description: "Adopt Zod for Boundary Schema Validation and Parsing: Modules Adopt Zod Schemas Runtime Input"
metadata:
  actual:
    adr_id: fb1f4c44-b9a3-4b3e-9582-b3b7e3ad7e50
    status: accepted
    candidate_group_id: fbb66e81-14fa-4010-b455-96af3f3a2042
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adopt Zod for Boundary Schema Validation and Parsing: Modules Adopt Zod Schemas Runtime Input

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MUST: Modules MUST adopt Zod schemas for runtime input validation and data boundary parsing.

### Verify

```bash
# Discover and run repository verification scripts to verify schema parse invocations execute successfully against test inputs.
npm test
```

**Accept when:**
- All input parsing invocations execute through defined validation schemas without unhandled validation failures on valid inputs.
- The project test suite passes with full verification of boundary inputs against declared schema specifications.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>