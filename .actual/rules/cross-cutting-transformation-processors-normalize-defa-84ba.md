---
version: 2
name: cross-cutting-transformation-processors-normalize-defa-84ba
description: "Internal Core Library Module Decomposition and Registry Pattern in Zod: Transformation Processors Normalize Default Value Definitions"
metadata:
  actual:
    adr_id: 84ba8f4d-9f7c-4f7f-9a12-f94e9eaad38b
    status: accepted
    candidate_group_id: fd8d8f66-6b2f-4c03-8911-bd9f1e5e7e6f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Internal Core Library Module Decomposition and Registry Pattern in Zod: Transformation Processors Normalize Default Value Definitions

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CORE-001** MAY: Transformation processors MAY normalize default value definitions and serialization artifacts through structured deep cloning mechanisms when immutability guarantees are required.

### Verify

```bash
# Discover and execute the repository test runner to validate recursive schema generation, registry lookups, and serialization behaviors.
# Discover and execute the repository module boundary and circular dependency verification scripts to ensure import isolation between core submodules.
# Discover and execute the repository static type checker to verify internal interface compatibility across all core module boundaries.
```

**Accept when:**
- All core module interfaces and internal imports resolve through the defined module boundaries without circular module initialization errors.
- Schema transformations and serializations correctly track cyclic structures using the contextual traversal cache without memory leaks.
- Static type checking and automated regression suites pass completely across all core library components.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated static analysis, module boundary linting, code review, and unit/integration test suites.
</enforcement>