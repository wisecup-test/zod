---
version: 2
name: cross-cutting-core-transformation-utilities-not-bypass-fd1d
description: "standard-schema Module Adoption: Core Transformation Utilities Not Bypass Standard"
metadata:
  actual:
    adr_id: fd1d5b1b-ccdd-4ac2-bb66-0d5ed1bac2a3
    status: accepted
    candidate_group_id: cde02561-665e-40aa-bc54-b52077956cb9
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# standard-schema Module Adoption: Core Transformation Utilities Not Bypass Standard

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for:
- All core schema transformation modules compiling or translating schemas across representation formats.
- All core error formatting and validation dispatch utilities requiring standardized schema contracts.

### Rules

- **R-LM-001** MUST_NOT: Core transformation utilities MUST NOT bypass standard-schema contracts by introducing direct circular dependencies to consumer-facing wrapper modules.

### Verify

- Discover the repository build and test script in the project manifest and execute the core test suite to verify contract compliance.
- Discover the repository linter and type-checker commands from project configuration and verify zero contract violations across core modules.

**Accept when:**

- All core schema transformations and error definitions pass automated type-checking and unit test suites verifying conformity to the standard-schema module contracts.
- Dependency analysis confirms no cyclic dependencies or direct bypasses of the standard-schema module in core schema transformation modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated static analysis checks enforcing module import boundaries and contract adherence.
- Verified by: Pull request architecture review validating separation of core module dependencies.
- Violation handling: Pull request builds fail if circular imports or standard-schema contract bypasses are introduced.
- Violation handling: Violations must be refactored to consume the centralized standard-schema module before merging.
- Exception process: Architectural exceptions require submitting a formal RFC justifying why standard-schema contracts cannot represent the necessary capability.
- Exception process: Exceptions must define isolated boundaries that do not leak proprietary signatures into standard transformation pipelines.
</enforcement>
