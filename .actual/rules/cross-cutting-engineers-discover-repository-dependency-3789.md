---
version: 2
name: cross-cutting-engineers-discover-repository-dependency-3789
description: "Zod Shared External Core Module Delegation: Engineers Discover Repository Dependency Resolution Artifact"
metadata:
  actual:
    adr_id: 37891c8c-4595-4f47-a1e1-0d9796ed1cb5
    status: accepted
    candidate_group_id: a85551aa-2a78-4339-85e4-5099508ef143
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/mini/**
      - src/v4-mini/**
---

# Zod Shared External Core Module Delegation: Engineers Discover Repository Dependency Resolution Artifact

Scope: applies to `packages/zod/src/mini/**`, `packages/zod/src/v4-mini/**`.

These rules are ALWAYS ACTIVE for:
- Modular and lightweight package entry point exports within the library workspace.
- Internal submodules providing public or semi-public validation surface definitions.

### Rules

- **R-LM-001** MUST: Engineers MUST discover the repository dependency resolution artifact to determine the exact resolved version of all internal workspace and library dependencies prior to referencing shared core exports.

### Verify

- Discover the repository build script from the project manifest and execute the compilation verification task to validate module export compatibility.
- Locate the project test runner configuration and execute the suite targeting modular entry point exports.
- Query the workspace static analysis configuration and run the module import linter to verify that lightweight entry facades import exclusively from the canonical external core module.

**Accept when:**

- All lightweight entry facades successfully compile and resolve exports against the canonical external core module without unresolved references.
- Automated test suites confirm behavioral equivalence across all modular export pathways.
- Static analysis checks pass with zero reported violations of module boundary delegation rules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline execution checking module export integrity and type signatures.
- Verified by: Peer code review validating that new entry facades delegate to the canonical external core module rather than duplicating runtime definitions.
- Verified by: Static analysis linting rules restricting direct internal cross-module dependencies.
- Violation handling: Pull requests introducing duplicate core implementations or bypassing the external core module are blocked from merging.
- Violation handling: Flagged architectural violations must be refactored to delegate directly to the canonical external core export.
- Exception process: Exceptions require written justification submitted via the architectural review workflow detailing why delegation is technically infeasible.
- Exception process: Approved exceptions must be time-bounded and documented within an architecture review record prior to code merge.
</enforcement>
