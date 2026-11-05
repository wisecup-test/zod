---
version: 2
name: cross-cutting-recursive-schema-transformations-leverag-672d
description: "standard-schema Module Adoption: Recursive Schema Transformations Leverage Contextual Memoization"
metadata:
  actual:
    adr_id: 672d643b-5080-4337-9f72-a5028e9415ac
    status: accepted
    candidate_group_id: cde02561-665e-40aa-bc54-b52077956cb9
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# standard-schema Module Adoption: Recursive Schema Transformations Leverage Contextual Memoization

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all core schema transformation modules compiling or translating schemas across representation formats, and all core error formatting and validation dispatch utilities requiring standardized schema contracts.

### Rules

- **R-SSM-001** SHOULD: Recursive schema transformations SHOULD leverage contextual memoization and metadata registry lookups when resolving standard-schema nodes.
- **R-SSM-002** MANDATORY: Core schema modules should consume transformation cache contexts and metadata registries uniformly when resolving schema identities.
- **R-SSM-003** MANDATORY: Error handling modules must derive standard issue structures through standard-schema abstractions to preserve cross-system compatibility.
- **R-SSM-004** MANDATORY (DISCOVERY POLICY): Omit all tool names, file names, commands, package managers, and version numbers in implementation; the consumer MUST derive them from the project repository.
- **R-SSM-005** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: (1) Find dependency manifest; (2) Identify build tool; (3) Inspect repository lock/resolution artifact for exact version; (4) Look up official documentation/changelog for that exact version; (5) Confirm every API, class, or function exists in that version's documentation; (6) Re-run steps 3-5 per dependency at point of use for version-sensitive behavior.

### Verify

```bash
# Discover the repository build and test script in the project manifest and execute the core test suite
# Discover the repository linter and type-checker commands from project configuration and verify zero contract violations
```

**Accept when:**
- All core schema transformations and error definitions pass automated type-checking and unit test suites verifying conformity to the standard-schema module contracts.
- Dependency analysis confirms no cyclic dependencies or direct bypasses of the standard-schema module in core schema transformation modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated static analysis checks enforcing module import boundaries and contract adherence, and pull request architecture review validating separation of core module dependencies. Violation handling: Pull request builds fail if circular imports or standard-schema contract bypasses are introduced, and violations must be refactored to consume the centralized standard-schema module before merging.
</enforcement>