---
version: 2
name: cross-cutting-validation-operations-employ-safe-parsin-549a
description: "Zod Schema-Based String Input Validation: Validation Operations Employ Safe Parsing Alternatives"
metadata:
  actual:
    adr_id: 549ae79b-a8c1-4559-9cb8-974a1a57b045
    status: accepted
    candidate_group_id: 054bbc9c-809f-42bc-8a1f-4ab536b9134b
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Zod Schema-Based String Input Validation: Validation Operations Employ Safe Parsing Alternatives

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for boundary handlers, resolution modules, and services receiving external or untrusted string inputs.

### Rules

- **R-ZOD-001** SHOULD: Validation operations SHOULD employ safe parsing alternatives where exception throwing on validation failure would degrade performance or disrupt expected error-handling workflows.
- **R-ZOD-002** MANDATORY: Define reusable schema objects at module scope rather than re-creating schemas inside request handlers.

### Verify

```bash
# Discover and run the project test suite to verify that schema validation tests pass
# Discover and run the project type checking and linting tasks to ensure type safety and rule compliance
```

**Accept when:**
- All test suites asserting schema parsing behavior pass with zero failures.
- Static analysis and type checking pass without errors or type assertion bypasses.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>