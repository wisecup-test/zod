---
version: 2
name: cross-cutting-exported-module-entry-points-execute-b53d
description: "Adopt Zod for Boundary Schema Validation and Parsing: Exported Module Entry Points Execute Schema"
metadata:
  actual:
    adr_id: b53d8af9-9630-4238-be63-5c80360ea990
    status: accepted
    candidate_group_id: fbb66e81-14fa-4010-b455-96af3f3a2042
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adopt Zod for Boundary Schema Validation and Parsing: Exported Module Entry Points Execute Schema

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for all public module interfaces, resolution entry points accepting external input data, and boundary parsing routines processing untrusted or polymorphic payloads.

### Rules

- **R-ZOD-001** MUST: Exported module entry points MUST execute schema parse operations on external inputs before passing data to internal components.

### Verify

```bash
# Discover and run the repository verification scripts to verify that all schema parse invocations execute successfully against test inputs.
# Execute the project test suite to verify that boundary validation logic correctly parses valid data and rejects invalid inputs.
```

**Accept when:**
- All input parsing invocations execute through defined validation schemas without unhandled validation failures on valid inputs.
- The project test suite passes with full verification of boundary inputs against declared schema specifications.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>