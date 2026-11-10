---
version: 2
name: cross-cutting-callers-not-bypass-schema-validation-1eb2
description: "Zod Schema-Based String Input Validation: Callers Not Bypass Schema Validation Asserting"
metadata:
  actual:
    adr_id: 1eb29373-e3f7-401c-9d5d-ff06660a7256
    status: accepted
    candidate_group_id: 054bbc9c-809f-42bc-8a1f-4ab536b9134b
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Zod Schema-Based String Input Validation: Callers Not Bypass Schema Validation Asserting

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for all boundary handlers, resolution modules, and services receiving external or untrusted string inputs.

### Rules

- **R-ZOD-001** MUST_NOT: Callers MUST_NOT bypass schema validation by asserting unvalidated string inputs as trusted domain types.
- **R-ZOD-002** MUST: Define reusable schema objects at module scope rather than re-creating schemas inside request handlers.
- **R-ZOD-003** MUST: Coordinate schema validation with boundary error mappers to format parsing rejections into standardized error responses.

### Verify

```bash
# Discover and run the project test suite to verify that schema validation tests pass.
# Discover and run the project type checking and linting tasks to ensure type safety and rule compliance.
```

**Accept when:**
- All test suites asserting schema parsing behavior pass with zero failures.
- Static analysis and type checking pass without errors or type assertion bypasses.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration test pipelines and automated static analysis enforce compliance, and violations block pull requests from merging.
</enforcement>