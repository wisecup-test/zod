---
version: 2
name: cross-cutting-schema-declarations-colocated-module-bou-06c2
description: "Adopt Zod for Boundary Schema Validation and Parsing: Schema Declarations Colocated Module Boundary Definitions"
metadata:
  actual:
    adr_id: 06c2f3e3-c61f-4f10-bcb6-98eca391fdbc
    status: accepted
    candidate_group_id: fbb66e81-14fa-4010-b455-96af3f3a2042
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adopt Zod for Boundary Schema Validation and Parsing: Schema Declarations Colocated Module Boundary Definitions

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for all public module interfaces, resolution entry points accepting external input data, and boundary parsing routines processing untrusted or polymorphic payloads.

### Rules

- **R-ZOD-001** SHOULD: Schema declarations SHOULD be colocated with module boundary definitions to maintain synchronization between static contracts and runtime rules.
- **R-ZOD-002** MANDATORY: The consumer MUST discover dependency management tools, manifests, and version locks directly from the repository.
- **R-ZOD-003** MANDATORY: Before writing code using a versioned library, execute the version-grounding check in order: find manifest, identify build tool, inspect lock/resolution artifact, look up official documentation for that exact version, and confirm API existence.
- **R-ZOD-004** MANDATORY: Define schemas alongside boundary interfaces and invoke schema parse operations at all entry points accepting external payloads.
- **R-ZOD-005** MANDATORY: Handle validation parse exceptions at the boundary layer to ensure structured error messages are returned to callers.

### Verify

```bash
# Discover and run repository verification scripts to test schema parse invocations
# Execute project test suite to verify boundary validation logic
```

**Accept when:**
- All input parsing invocations execute through defined validation schemas without unhandled validation failures on valid inputs.
- The project test suite passes with full verification of boundary inputs against declared schema specifications.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests with unvalidated boundary inputs or manual type assertions will be blocked until schema validation is introduced.
</enforcement>