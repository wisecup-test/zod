---
version: 2
name: cross-cutting-modules-not-bypass-schema-parse-6d0e
description: "Adoption of Zod for Runtime Schema Declaration and Input Validation: Modules Not Bypass Schema Parse Operations"
metadata:
  actual:
    adr_id: 6d0e63cb-d750-4b76-bc2a-f139cd3bf46b
    status: accepted
    candidate_group_id: 1a1e2218-cf8b-4cc0-bc62-7046d6a5fe5c
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Adoption of Zod for Runtime Schema Declaration and Input Validation: Modules Not Bypass Schema Parse Operations

Scope: applies to `packages/treeshake/**`.

These rules are ALWAYS ACTIVE for:
- All modules and packages defining data models that parse or ingest external or untrusted inputs.
- Internal boundaries requiring explicit schema contracts and runtime type validation.

### Rules

- **R-LM-001** MUST_NOT: Modules MUST NOT bypass schema parse operations when accepting untrusted external payload data.

### Verify

- Discover the repository script runner and execute the project verification test suite to ensure all schema validation tests pass.
- Discover the static analysis check defined in the project configuration and execute type checking to verify that schema inference aligns with declared data contracts.

**Accept when:**

- All discovered schema validation test suites execute and report zero failures.
- Static type analysis confirms that data types inferred from schemas match expected input contracts across all consumption boundaries.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated test suites executing schema parsing validations during continuous integration.
- Verified by: Code review checks verifying that all external data ingress points apply schema parsing.
- Violation handling: Pull requests lacking schema validation at untrusted input boundaries will be blocked until compliant schemas and tests are added.
- Exception process: Exceptions must be submitted via architectural review with documented performance benchmarking and justification.
</enforcement>
