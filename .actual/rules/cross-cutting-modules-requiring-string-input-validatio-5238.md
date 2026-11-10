---
version: 2
name: cross-cutting-modules-requiring-string-input-validatio-5238
description: "Zod Schema-Based String Input Validation: Modules Requiring String Input Validation Construct"
metadata:
  actual:
    adr_id: 5238c468-2f45-4b85-9b6a-633304f8f8dd
    status: accepted
    candidate_group_id: 054bbc9c-809f-42bc-8a1f-4ab536b9134b
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Zod Schema-Based String Input Validation: Modules Requiring String Input Validation Construct

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for all boundary handlers, resolution modules, and services receiving external or untrusted string inputs.

### Rules

- **R-ZOD-001** MUST: Modules requiring string input validation MUST construct Zod schemas using string definitions and enforce validation prior to passing values to internal domain logic.

### Verify

```bash
# Discover and run the project test suite to verify that schema validation tests pass.
# Discover and run the project type checking and linting tasks to ensure type safety and rule compliance.
```

**Accept when:**
- All test suites asserting schema parsing behavior pass with zero failures.
- Static analysis and type checking pass without errors or type assertion bypasses.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>