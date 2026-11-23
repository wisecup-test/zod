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

These rules are ALWAYS ACTIVE for:
- Boundary handlers, resolution modules, and services receiving external or untrusted string inputs.

### Rules

- **R-SCP-001** SHOULD: Validation operations SHOULD employ safe parsing alternatives where exception throwing on validation failure would degrade performance or disrupt expected error-handling workflows.

### Verify

- Discover and run the project test suite to verify that schema validation tests pass.
- Discover and run the project type checking and linting tasks to ensure type safety and rule compliance.

**Accept when:**

- All test suites asserting schema parsing behavior pass with zero failures.
- Static analysis and type checking pass without errors or type assertion bypasses.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Continuous integration test pipelines and automated static analysis.
- Verified by: Peer code reviews on pull requests modifying boundary input handling.
- Violation handling: Pull requests lacking required boundary schema validation are blocked from merging until compliant schemas are introduced.
- Exception process: Exceptions require approval from the security architecture lead with documented rationale demonstrating equivalent boundary sanitization.
</enforcement>
