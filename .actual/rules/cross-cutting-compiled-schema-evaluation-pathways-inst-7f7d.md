---
version: 2
name: cross-cutting-compiled-schema-evaluation-pathways-inst-7f7d
description: "Internal Core Module Architecture for Schema Engine and Processing Subsystems: Compiled Schema Evaluation Pathways Install Execution"
metadata:
  actual:
    adr_id: 7f7d6cf2-75b5-4a4b-9d12-8a6ac8220f8c
    status: accepted
    candidate_group_id: 6af386df-1645-4617-9e12-ca356ef23697
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module Architecture for Schema Engine and Processing Subsystems: Compiled Schema Evaluation Pathways Install Execution

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for internal library modules implementing core schema primitives, registries, error handlers, and utility routines, as well as compiler and format conversion subsystems interacting with foundational schema models.

### Rules

- **R-CORE-001** SHOULD: Compiled schema evaluation pathways install compiled execution methods over runtime parsers while preserving fallback behavior when invalid markers are encountered.
- **R-CORE-002** MANDATORY: The consumer MUST derive tool names, file names, commands, package managers, and version numbers from the project repository according to the discovery policy.
- **R-CORE-003** MANDATORY: Before writing code that uses a versioned library, execute in order: find the dependency manifest in the repo, identify the build tool, inspect the repository lock or resolution artifact for the exact resolved version, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run steps per dependency at point of use.
- **R-CORE-004** MANDATORY: Ensure core module exports expose stable interfaces for schemas, registries, and error constructs that external modules can depend upon reliably.
- **R-CORE-005** MANDATORY: Maintain isolated registry and traversal context lifecycles during compilation and conversion routines to avoid memory leaks or state contamination.

### Verify

```bash
# Run the project test suite to verify internal core module boundaries and schema compilation passes all functional suites.
# Execute the repository linting and module boundary checks to ensure no circular imports or disallowed core module references exist.
# Execute the project typechecker to confirm strict type safety across core schema exports and registry interfaces.
```

**Accept when:**
- All internal module boundary tests and schema validation suites pass without errors.
- Dependency and type validation checks complete with zero circular reference or boundary violations.
- Runtime compilation methods match baseline parser behavior for all defined schema inputs.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by static module boundary analysis, peer review, and automated unit/integration test coverage.
</enforcement>