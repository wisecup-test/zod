---
version: 2
name: cross-cutting-before-implementing-features-dependent-v-0d4e
description: "Core Module Architecture for Shared Schema Primitives: Before Implementing Features Dependent Versioned External"
metadata:
  actual:
    adr_id: 0d4e0e89-7f98-49a0-a1cc-4fd6a689b7ad
    status: accepted
    candidate_group_id: bec2016e-3f8a-44fb-95a3-11cf67256d04
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Core Module Architecture for Shared Schema Primitives: Before Implementing Features Dependent Versioned External

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for:
- All internal schema distributions, flavor entrypoints, and shared utility modules within the library architecture.

### Rules

- **R-LM-001** MUST: Before implementing features dependent on versioned external dependencies, the consumer MUST discover the repository lock artifact and verify the exact resolved version.

### Verify

- Discover and execute the project boundary analysis check to confirm that all shared imports originate from the core module.
- Discover and run the repository test and validation suite to verify that all distribution flavors successfully integrate with the core module.

**Accept when:**

- Dependency boundary analysis passes with zero cross-flavor couplings and all shared traversal logic referencing the core module.
- Repository test suites execute successfully with all modules resolving core registry and utility contracts.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated boundary and module resolution checks in the continuous integration pipeline.
- Verified by: Architecture review during pull requests verifying adherence to core import layers.
- Violation handling: Pull requests containing direct cross-flavor imports or duplicated traversal logic are blocked.
- Violation handling: Violations must be remediated by extracting common primitives into the core module.
- Exception process: Submit an architectural exception request detailing why a capability cannot reside within the core module or why an alternative boundary is necessary.
- Exception process: Obtain sign-off from library maintainers prior to merging any cross-distribution import paths.
</enforcement>
