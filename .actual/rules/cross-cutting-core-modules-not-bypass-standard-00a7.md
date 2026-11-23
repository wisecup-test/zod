---
version: 2
name: cross-cutting-core-modules-not-bypass-standard-00a7
description: "Standard Schema Interface Adoption: Core Modules Not Bypass Standard Schema"
metadata:
  actual:
    adr_id: 00a74422-e978-4e81-a445-d431d06bfa18
    status: accepted
    candidate_group_id: 1044d40f-34d5-44f9-a360-a138cf5e1eb0
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Standard Schema Interface Adoption: Core Modules Not Bypass Standard Schema

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for:
- Core schema definition modules, validation engines, and error normalization pipelines.
- Serialization adapters and schema introspection utilities translating validation definitions to external formats.

### Rules

- **R-LM-001** MUST_NOT: Core modules MUST NOT bypass Standard Schema contracts when exposing schema inspection or metadata access to external consumers or serialization adapters.

### Verify

- Discover and execute the project repository static type verification suite to confirm interface conformance across all core modules.
- Execute the project automated test suite to ensure schema transformation and error reporting behavior complies with specification contracts.

**Accept when:**

- All core schema compilation, error handling, and serialization modules pass static type verification without interface mismatches.
- Automated unit and integration test suites succeed with zero regressions in schema validation or issue formatting.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Continuous integration pipelines executing static type analysis and automated test suites on all code contributions.
- Verified by: Peer architectural reviews verifying contract compliance against the Standard Schema specification during pull request evaluation.
- Violation handling: Contributions introducing proprietary validation interfaces or non-compliant issue structures are rejected during continuous integration checks.
- Violation handling: Non-conforming implementations must be refactored to align with the Standard Schema interface contract prior to merge approval.
- Exception process: Architectural exceptions require formal review and unanimous approval by the architecture engineering group with documented technical justification and an agreed-upon remediation timeline.
</enforcement>
