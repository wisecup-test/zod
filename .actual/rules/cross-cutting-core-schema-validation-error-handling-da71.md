---
version: 2
name: cross-cutting-core-schema-validation-error-handling-da71
description: "Standard Schema Interface Adoption: Core Schema Validation Error Handling Serialization"
metadata:
  actual:
    adr_id: da718461-e8fb-43a1-9895-ef5439db94fd
    status: accepted
    candidate_group_id: 1044d40f-34d5-44f9-a360-a138cf5e1eb0
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Standard Schema Interface Adoption: Core Schema Validation Error Handling Serialization

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema definition modules, validation engines, error normalization pipelines, serialization adapters, and schema introspection utilities.

### Rules

- **R-SS-001** MUST: Core schema validation, error handling, and serialization modules MUST adopt the Standard Schema specification interface as the primary contract for schema execution, error normalization, and metadata registration.
- **R-SS-002** MANDATORY: Execute the DISCOVERY POLICY to derive tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-SS-003** MANDATORY: Execute the LOCK-VERSION GROUNDING procedure in order (manifest -> build tool -> lock/resolution artifact -> version-specific docs -> API confirmation) before writing code that uses a versioned library.
- **R-SS-004** MUST: Inspect the repository dependency graph to identify existing schema metadata registries and caching layers before implementing new transformation adapters.
- **R-SS-005** MUST: Ensure all schema traversal procedures incorporate cache lookups and prototype safety guards to handle recursive definitions safely.

### Verify

```bash
# Discover and execute the project repository static type verification suite to confirm interface conformance across all core modules.
# Execute the project automated test suite to ensure schema transformation and error reporting behavior complies with specification contracts.
```

**Accept when:**
- All core schema compilation, error handling, and serialization modules pass static type verification without interface mismatches.
- Automated unit and integration test suites succeed with zero regressions in schema validation or issue formatting.

<enforcement>
Claude Code MUST NOT skip or defer verification. Contributions introducing proprietary validation interfaces or non-compliant issue structures are rejected during continuous integration checks. Non-conforming implementations must be refactored to align with the Standard Schema interface contract prior to merge approval. Architectural exceptions require formal review and unanimous approval by the architecture engineering group with documented technical justification and an agreed-upon remediation timeline.
</enforcement>