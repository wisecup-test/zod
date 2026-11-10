---
version: 2
name: cross-cutting-schema-definitions-type-checking-modules-ad8d
description: "Adoption of json-schema-processors Core Module Architecture: Schema Definitions Type Checking Modules Not"
metadata:
  actual:
    adr_id: ad8d6650-2a00-4457-bbf6-b83d58190b76
    status: accepted
    candidate_group_id: 4f3aa984-f581-4fab-b688-1e6017994f30
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Adoption of json-schema-processors Core Module Architecture: Schema Definitions Type Checking Modules Not

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-JSON-001** MUST_NOT: Schema definitions and type checking modules MUST NOT embed inline JSON schema generation logic outside the dedicated core processor and generator modules.

### Verify

```bash
# Discover and run the project repository validation suite for core module type-checking and unit test suites
# Discover and execute the repository integration test suite verifying JSON schema generation across complex and cyclic schema fixtures
```

**Accept when:**
- All unit tests for schema processors and generators pass without errors or circular reference exceptions.
- Static type analysis across all core modules completes with zero diagnostic warnings or type mismatch errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration pipeline and peer code review.
</enforcement>