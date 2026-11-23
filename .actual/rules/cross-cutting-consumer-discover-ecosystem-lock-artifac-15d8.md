---
version: 2
name: cross-cutting-consumer-discover-ecosystem-lock-artifac-15d8
description: "Internal Core Module for Shared Validation Primitives: Consumer Discover Ecosystem Lock Artifact Verify"
metadata:
  actual:
    adr_id: 15d8289f-84a7-41b7-aed0-34ced7df5b7b
    status: accepted
    candidate_group_id: 6f1a4916-3848-4f86-b843-16c190a6b899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module for Shared Validation Primitives: Consumer Discover Ecosystem Lock Artifact Verify

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for:
- Implementation of localization dictionaries and error message mappings
- Implementation of schema adapters and compatibility translation layers
- Creation of peripheral extensions requiring shared validation checks or error structures

### Rules

- **R-LM-001** MUST: The consumer MUST discover the ecosystem lock artifact and verify all resolved dependency versions before implementing or modifying module boundaries.

### Verify

- Discover the project verification script from the repository manifest and execute static analysis to validate module import paths.
- Discover and run the project test suite to verify that all localization and compatibility modules satisfy core module interface contracts.

**Accept when:**

- Static analysis confirms zero circular dependencies and verifies all peripheral modules import shared primitives from the internal core module.
- All automated test suites pass without interface contract mismatches or unhandled validation errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration checks validating static import boundaries.
- Verified by: Peer code review for all pull requests modifying core interfaces or adding localization files.
- Violation handling: Continuous integration builds fail upon detection of unauthorized dependency paths or duplicate validation primitives.
- Violation handling: Pull requests violating inward module boundaries are blocked until refactored.
- Exception process: Submit an architectural review request detailing technical constraints preventing reliance on the core module.
- Exception process: Temporary exceptions require formal sign-off from the core architecture team with a scheduled remediation plan.
</enforcement>
