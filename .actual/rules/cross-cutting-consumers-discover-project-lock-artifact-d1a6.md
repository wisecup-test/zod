---
version: 2
name: cross-cutting-consumers-discover-project-lock-artifact-d1a6
description: "Adopt Zod for Boundary Schema Validation and Parsing: Consumers Discover Project Lock Artifact Resolve"
metadata:
  actual:
    adr_id: d1a6dec0-4658-4efa-a060-9e880032f637
    status: accepted
    candidate_group_id: fbb66e81-14fa-4010-b455-96af3f3a2042
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adopt Zod for Boundary Schema Validation and Parsing: Consumers Discover Project Lock Artifact Resolve

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for all public module interfaces, resolution entry points, and boundary parsing routines accepting external input data.

### Rules

- **R-ZOD-001** MUST: Consumers MUST discover the project lock artifact and resolve the exact locked version of the schema validation library before implementation.
- **R-ZOD-002** MUST: Define schemas alongside boundary interfaces and invoke schema parse operations at all entry points accepting external payloads.
- **R-ZOD-003** MUST: Handle validation parse exceptions at the boundary layer to ensure structured error messages are returned to callers.

### Verify

```bash
# Discover and run repository verification scripts to test schema parse invocations
# Execute project test suite to verify boundary validation logic
 npm test
```

**Accept when:**
- All input parsing invocations execute through defined validation schemas without unhandled validation failures on valid inputs.
- The project test suite passes with full verification of boundary inputs against declared schema specifications.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>