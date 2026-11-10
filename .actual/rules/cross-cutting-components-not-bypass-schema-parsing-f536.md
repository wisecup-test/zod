---
version: 2
name: cross-cutting-components-not-bypass-schema-parsing-f536
description: "Adoption of Zod for Schema Definition and Input Validation: Components Not Bypass Schema Parsing Use"
metadata:
  actual:
    adr_id: f5368f99-0d67-4b4d-9349-3247a838c66e
    status: accepted
    candidate_group_id: d82ab627-4321-406c-a644-2305a03bee19
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of Zod for Schema Definition and Input Validation: Components Not Bypass Schema Parsing Use

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MUST_NOT: Components MUST NOT bypass schema parsing or use unvalidated type casting on data ingested across boundaries.

### Verify

```bash
# Discover and run the project's verification and test scripts from the repository manifest
# Example discovery:
TEST_SCRIPT=$(npm pkg get scripts.test --json 2>/dev/null || echo "test")
eval "npm test"
```

**Accept when:**
- All schema validation parsing logic executes successfully across all supported module targets.
- Repository verification scripts complete with zero exit codes and no schema parsing errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. All runtime input validation must utilize schema parsing without bypassing boundary checks.
</enforcement>