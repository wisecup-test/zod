---
version: 2
name: cross-cutting-registry-implementations-maintaining-bid-485a
description: "Internal Schema Metadata Registries Module for Contextual State and Bidirectional Identity Storage: Registry Implementations Maintaining Bidirectional Identifier Schema"
metadata:
  actual:
    adr_id: 485a1265-82d1-4de2-b3d9-3b7971e8b42d
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

# Internal Schema Metadata Registries Module for Contextual State and Bidirectional Identity Storage: Registry Implementations Maintaining Bidirectional Identifier Schema

Scope: applies to `packages/zod/src/v3/**`, `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all schema processing, serialization, deserialization, and compilation workflows involving metadata associations and bidirectional identifier tracking.

### Rules

- **R-REG-001** SHOULD: Registry implementations maintaining bidirectional identifier-to-schema lookups SHOULD synchronize both primary and inverse index collections atomically during registration and deregistration.
- **R-REG-002** MANDATORY: Schema definitions MUST remain strictly immutable and thread-safe across concurrent validations by isolating schema-to-metadata associations and bidirectional identifier indices into dedicated registry structures with explicit lifecycle boundaries.
- **R-REG-003** MANDATORY: Traversal contexts MUST be instantiated at the root of translation or compilation workflows and passed context instances explicitly down recursive visitor calls.
- **R-REG-004** MANDATORY: Recursive traversal calls MUST wrap in structured exception-handling blocks that guarantee deterministic cleanup of tracking references and prevent memory retention upon scope exit or exceptional termination.
- **R-REG-005** MANDATORY: Developers MUST derive all tool names, file names, commands, package managers, and version numbers directly from the project repository following the discovery policy and lock-version grounding sequence before writing code using a versioned library.

### Verify

```bash
# Discover workspace test execution script in project manifest and run schema registries and compiler traversal suite
# Discover repository static analysis script and verify zero direct property mutations on schema instances across data access modules
```

**Accept when:**
- All registry unit and integration test suites pass with complete assertion coverage on bidirectional lookup, registration, and deletion.
- Memory profiling tests confirm traversal context maps release all tracking references upon traversal completion without leakage.
- Static type checks verify that schema definitions remain read-only and all external metadata access occurs through registry abstractions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated unit and integration test runs, peer code reviews, and static analysis checks enforce registry data access patterns and recursion cleanup logic.
</enforcement>