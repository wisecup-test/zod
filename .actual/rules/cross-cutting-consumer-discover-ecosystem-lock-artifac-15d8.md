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

These rules are ALWAYS ACTIVE for all localization dictionaries, schema adapters, compatibility translation layers, and peripheral extensions requiring shared validation checks or error structures.

### Rules

- **R-CORE-001** MUST: The consumer MUST discover the ecosystem lock artifact and verify all resolved dependency versions before implementing or modifying module boundaries.
- **R-CORE-002** MUST: Ensure newly authored localization dictionaries import error definitions and validation checks exclusively from the core module namespace.
- **R-CORE-003** MUST: Verify that all imported core utility methods and visitor contracts preserve backward compatibility when extending schema traversal logic.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute static analysis
# Discover and run the project test suite to verify that all localization and compatibility modules satisfy core module interface contracts
```

**Accept when:**
- Static analysis confirms zero circular dependencies and verifies all peripheral modules import shared primitives from the internal core module.
- All automated test suites pass without interface contract mismatches or unhandled validation errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>