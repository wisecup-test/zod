---
version: 2
name: cross-cutting-boundary-interfaces-not-rely-exclusively-475c
description: "Adopt Zod for Boundary Schema Validation and Parsing: Boundary Interfaces Not Rely Exclusively Static"
metadata:
  actual:
    adr_id: 475c66b8-d659-4611-8906-b317f61ce949
    status: accepted
    candidate_group_id: fbb66e81-14fa-4010-b455-96af3f3a2042
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adopt Zod for Boundary Schema Validation and Parsing: Boundary Interfaces Not Rely Exclusively Static

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for all public module interfaces, resolution entry points, and boundary parsing routines accepting external input data.

### Rules

- **R-BND-001** MUST_NOT: Boundary interfaces MUST_NOT rely exclusively on static type assertions without runtime schema parsing.

### Verify

```bash
# Discover and run the repository verification scripts to verify that all schema parse invocations execute successfully against test inputs.
# Execute the project test suite to verify that boundary validation logic correctly parses valid data and rejects invalid inputs.
# (Exact commands must be discovered from the project repository per the discovery policy)
```

**Accept when:**
- All input parsing invocations execute through defined validation schemas without unhandled validation failures on valid inputs.
- The project test suite passes with full verification of boundary inputs against declared schema specifications.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>