---
version: 2
name: cross-cutting-validation-schemas-construct-primitive-o-62c8
description: "Adoption of zod/mini for Functional and Tree-Shakeable Schema Validation: Validation Schemas Construct Primitive Object Validators"
metadata:
  actual:
    adr_id: 62c84f20-96cf-4511-8f76-0d68c2db1fbb
    status: accepted
    candidate_group_id: 4ecfb3a9-b029-42f8-9301-7d71eb684470
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Adoption of zod/mini for Functional and Tree-Shakeable Schema Validation: Validation Schemas Construct Primitive Object Validators

Scope: applies to `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for:
- Input validation layers and data parsing modules across the codebase.
- Runtime schema definitions for structured and primitive payload verification.

### Rules

- **R-LM-001** MUST: Validation schemas MUST construct primitive and object validators using z.string, z.number, z.boolean, and z.object from the functional entrypoint.

### Verify

- Discover the project dependency manifest and lock file to inspect the declared and resolved module entries for the schema validation library.
- Execute the project automated test suite via the repository script runner to validate schema parsing assertions.
- Run the project static type checker and linter to ensure all schema definitions adhere to functional entrypoint constraints.

**Accept when:**

- All schema validation invocations resolve through the modular functional entrypoint without importing monolithic packages.
- Input parsing tests successfully verify structural and constraint assertions using schema parse methods.
- Static analysis and type checking pass without errors across all modules declaring validation schemas.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated test suites asserting runtime schema validation and rejection behavior.
- Verified by: Static analysis import rules verifying that schema imports use the functional entrypoint.
- Verified by: Peer code review for new schema definitions and boundary validation logic.
- Violation handling: Pull requests importing non-modular entrypoints are blocked by static analysis checks.
- Violation handling: Unvalidated data inputs at system boundaries trigger test failures requiring schema enforcement.
- Exception process: Exceptions require documented justification demonstrating why modular schema validation cannot satisfy runtime constraints, approved by architecture review.
</enforcement>
