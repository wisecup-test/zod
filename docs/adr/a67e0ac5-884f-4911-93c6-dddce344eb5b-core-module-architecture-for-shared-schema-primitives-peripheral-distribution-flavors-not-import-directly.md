---
version: 2
name: a67e0ac5-884f-4911-93c6-dddce344eb5b-core-module-architecture-for-shared-schema-primitives-peripheral-distribution-flavors-not-import-directly
description: "Core Module Architecture for Shared Schema Primitives: Peripheral Distribution Flavors Not Import Directly"
metadata:
  actual:
    adr_id: a67e0ac5-884f-4911-93c6-dddce344eb5b
    status: accepted
    candidate_group_id: bec2016e-3f8a-44fb-95a3-11cf67256d04
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Core Module Architecture for Shared Schema Primitives: Peripheral Distribution Flavors Not Import Directly

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v4/**`

## Context

- Multiple distinct library distribution flavors require shared schema mechanics, AST traversal algorithms, and central metadata registries.
- Direct coupling between peripheral distribution flavors causes circular dependencies and redundant logic.
- Centralizing shared schema primitives and registry storage in an internal core module provides a stable foundation across entrypoints.

## Problem Statement

Independent library flavors and entrypoint modules require identical schema traversal logic, checks, and metadata registries, creating a risk of redundant code and behavioral divergence if shared primitives are not centralized behind a unified architectural layer.

## Decision

1. MUST_NOT: Peripheral distribution flavors MUST NOT import directly from sibling distribution flavors to access shared parsing or traversal logic.

## Policy Block

- MUST_NOT Peripheral distribution flavors MUST NOT import directly from sibling distribution flavors to access shared parsing or traversal logic.

In scope:
- All internal schema distributions, flavor entrypoints, and shared utility modules within the library architecture.

Out of scope:
- End-user application consumer code outside the internal library implementation boundaries.

## Rationale

- Consolidating traversal functions, error utilities, and global registries in the core module guarantees consistent schema processing semantics across all distribution flavors.
- Structuring dependencies unidirectionally from flavors into the core module prevents cyclic references and clarifies library component responsibilities.

## Consequences

Positive:
- Centralizes critical parsing, traversal algorithms, and schema registries into a single authoritative module.
- Eliminates redundant implementations across diverse entrypoint distributions.
- Enforces unidirectional architectural dependencies from peripheral distributions into the core engine.

Negative:
- Changes to core module interfaces require synchronized updates and regression verification across all dependent distribution flavors.
- Distribution packages carry an architectural dependency on internal core contracts that must be preserved during refactoring.

## Alternatives

- Duplicate traversal utilities and registry definitions independently across each distribution flavor (rejected)
  Rejected because: Creates maintenance divergence and risks inconsistent runtime validation and registry behavior across distributions
  When valid: When distributions must have entirely zero runtime shared memory and isolated standalone implementations
- Direct peer-to-peer consumption between distribution modules without an intermediate core layer (rejected)
  Rejected because: Introduces tight bidirectional coupling and circular dependencies between distinct API flavors
  When valid: When only a single monolithic distribution is maintained

## Risks

- Breaking modifications in the internal core module can unintentionally destabilize multiple dependent consumer distributions.
  Mitigation: Maintain comprehensive regression test suites across all consuming distributions whenever core primitives or registries change.
  Owner: engineering team
- Inadvertent leakage of internal core APIs into the public API surface can create unintended external breaking change liabilities.
  Mitigation: Apply strict internal export boundaries to avoid exposing internal core abstractions as public library API contracts.
  Owner: engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Ensure core module exports expose minimal, highly cohesive utilities and registries required by consumers.
- Maintain unidirectional module references so that the core module never depends on consumer distributions.

## Continuation Context


Verify commands:
- Discover and execute the project boundary analysis check to confirm that all shared imports originate from the core module.
- Discover and run the repository test and validation suite to verify that all distribution flavors successfully integrate with the core module.

Accept when:
- Dependency boundary analysis passes with zero cross-flavor couplings and all shared traversal logic referencing the core module.
- Repository test suites execute successfully with all modules resolving core registry and utility contracts.

## Enforcement

- Verified by: Automated boundary and module resolution checks in the continuous integration pipeline.
- Verified by: Architecture review during pull requests verifying adherence to core import layers.
- Violation handling: Pull requests containing direct cross-flavor imports or duplicated traversal logic are blocked.
- Violation handling: Violations must be remediated by extracting common primitives into the core module.
- Exception process: Submit an architectural exception request detailing why a capability cannot reside within the core module or why an alternative boundary is necessary.
- Exception process: Obtain sign-off from library maintainers prior to merging any cross-distribution import paths.