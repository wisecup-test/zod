---
version: 2
name: cross-cutting-before-implementing-validation-logic-thi-eecf
description: "Zod Schema-Based String Input Validation: Before Implementing Validation Logic Third Party"
metadata:
  actual:
    adr_id: eecf273f-964e-4f49-bfef-7b4d77923ab3
    status: accepted
    candidate_group_id: 054bbc9c-809f-42bc-8a1f-4ab536b9134b
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Zod Schema-Based String Input Validation: Before Implementing Validation Logic Third Party

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for:
- Boundary handlers, resolution modules, and services receiving external or untrusted string inputs.

### Rules

- **R-SCP-001** MUST: Before implementing validation logic with a third-party schema library, the consumer MUST inspect the repository lock artifact to verify the exact resolved version and adhere to its published API specification.

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
