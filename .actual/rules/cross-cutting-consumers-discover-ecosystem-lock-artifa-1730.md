---
version: 2
name: cross-cutting-consumers-discover-ecosystem-lock-artifa-1730
description: "Valibot Schema Validation Adoption: Consumers Discover Ecosystem Lock Artifact Verify"
metadata:
  actual:
    adr_id: 173094f6-4a03-463f-a9ef-8a785552b92a
    status: accepted
    candidate_group_id: dc6286a1-b983-49d4-82ec-9f40035aa215
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Valibot Schema Validation Adoption: Consumers Discover Ecosystem Lock Artifact Verify

Scope: applies to `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for:
- Modules defining data schemas, input parsing, and runtime boundary validation.
- Components requiring modular schema verification and tree-shakeable packaging.

### Rules

- **R-LM-001** MUST: Consumers MUST discover the ecosystem lock artifact and verify the exact resolved version of the validation library before invoking any schema definition APIs.

### Verify

- Discover the project test runner configuration from the repository manifest and execute the validation test suite.
- Discover the static analysis and type verification script from the repository manifest and run it to verify schema compilation.
- Discover the build bundle inspection script from repository configuration and execute it to verify modular tree-shaking compliance.

**Accept when:**

- All schema validation test suites execute and pass without validation or runtime errors.
- Static type checking completes with zero type errors for all inferred schema types.
- Bundle inspection confirms unused validation functions are eliminated from production output.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline running test suites and bundle size checks.
- Verified by: Static analysis and type checking during repository build verification.
- Verified by: Architecture and peer review on pull requests touching schema definitions.
- Violation handling: Pull requests introducing non-compliant validation libraries or unbundled namespace imports will fail continuous integration checks and be blocked from merging.
- Violation handling: Violations discovered in existing code must be logged as technical debt and refactored to standard modular schema patterns.
- Exception process: Submit an architectural deviation request documenting protocol constraints and performance justifications to the Architecture Review Board for formal evaluation.
</enforcement>
