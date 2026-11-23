---
version: 2
name: cross-cutting-schema-transformation-compilation-routin-5d6e
description: "Internal Schema Metadata Registries Module for Contextual State and Bidirectional Identity Storage: Schema Transformation Compilation Routines Not Attach"
metadata:
  actual:
    adr_id: 5d6e8a33-c66e-431f-b5ff-9f8e6d1dc341
    status: accepted
    candidate_group_id: d8b3ef21-85e1-4a50-9fc9-84f24d157d45
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
      - src/v4/**
---

# Internal Schema Metadata Registries Module for Contextual State and Bidirectional Identity Storage: Schema Transformation Compilation Routines Not Attach

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for:
- Schema metadata association and external identifier resolution.
- Recursive schema serialization and deserialization involving circular reference tracking.
- Compiler constant registration and variable scope isolation during schema code generation.

### Rules

- **R-DAP-001** MUST_NOT: Schema transformation and compilation routines MUST NOT attach transient traversal state, intermediate constants, or resolved references directly to schema instances as mutable properties.

### Verify

- Discover the workspace test execution script in the project manifest and run the suite covering schema registries and compiler traversal.
- Discover the repository static analysis script and verify zero direct property mutations on schema instances across data access modules.

**Accept when:**

- All registry unit and integration test suites pass with complete assertion coverage on bidirectional lookup, registration, and deletion.
- Memory profiling tests confirm traversal context maps release all tracking references upon traversal completion without leakage.
- Static type checks verify that schema definitions remain read-only and all external metadata access occurs through registry abstractions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated unit and integration test runs executed during continuous integration workflows.
- Verified by: Peer code reviews auditing registry data access patterns and recursion cleanup logic.
- Verified by: Static analysis checks detecting unauthorized property assignments to schema definition objects.
- Violation handling: Code review rejection for pull requests that mutate schema instances directly to store state.
- Violation handling: Automated continuous integration failures when bidirectional registry indices fail synchronization invariants.
- Exception process: Submit an architectural review request detailing why registry-based access is impractical for the specific isolated evaluation path.
- Exception process: Obtain explicit sign-off from the technical lead with documented memory profiling and immutability impact assessments.
</enforcement>
