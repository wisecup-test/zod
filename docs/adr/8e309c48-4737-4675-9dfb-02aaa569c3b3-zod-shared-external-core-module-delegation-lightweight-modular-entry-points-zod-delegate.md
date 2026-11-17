---
version: 2
name: 8e309c48-4737-4675-9dfb-02aaa569c3b3-zod-shared-external-core-module-delegation-lightweight-modular-entry-points-zod-delegate
description: "Zod Shared External Core Module Delegation: Lightweight Modular Entry Points Zod Delegate"
metadata:
  actual:
    adr_id: 8e309c48-4737-4675-9dfb-02aaa569c3b3
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

# Zod Shared External Core Module Delegation: Lightweight Modular Entry Points Zod Delegate

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/mini/**`
- `src/v4-mini/**`

## Context

- The codebase provides modular lightweight distribution variants alongside standard library entry points to optimize downstream bundle footprints.
- Multiple entry points requiring consistent core schema capabilities risk divergence and maintenance overhead if runtime primitives are independently defined.
- Static analysis observes multiple modular entry points converging on a shared external core module import to provide unified export surfaces.

## Problem Statement

Maintaining independent core validation primitives across distinct entry points causes logic divergence, increases maintenance overhead, and inflates bundle sizes for consumers importing modular entry points.

## Decision

1. MUST: Lightweight modular entry points for Zod MUST delegate core schema capabilities directly to the centralized shared external core module rather than implementing independent runtime logic.

## Policy Block

- MUST Lightweight modular entry points for Zod MUST delegate core schema capabilities directly to the centralized shared external core module rather than implementing independent runtime logic.

In scope:
- Modular and lightweight package entry point exports within the library workspace.
- Internal submodules providing public or semi-public validation surface definitions.

Out of scope:
- Internal standalone utility helpers that do not expose public schema primitives.
- Full-bundle monolithic distribution entry points with independent top-level bindings.

## Rationale

- Delegating to a single external core module eliminates logic duplication and ensures identical schema behavior across all lightweight entry surfaces.
- Centralizing external primitives simplifies API evolution and guarantees that performance optimizations or bug fixes propagate uniformly to all consumer-facing modular facades.
- The pattern preserves lean modular entry facades while keeping the underlying runtime implementation strictly cohesive.

## Consequences

Positive:
- Guarantees behavioral and schema validation consistency across all lightweight module entry points.
- Eliminates duplication of foundational validation primitives, reducing overall package footprint.
- Establishes clear architectural separation between consumer-facing entry facades and core external implementations.

Negative:
- Couples modular entry facades to the internal structure and export contracts of the shared external core module.
- Requires strict boundary governance to ensure entry facades do not inadvertently pull in unwanted transitive internal dependencies.

## Alternatives

- Independent runtime implementations per entry point (rejected)
  Rejected because: Duplicating core validation logic across variant entry points creates behavioral drift and doubles ongoing maintenance overhead.
  When valid: Only when modular variants have completely distinct, incompatible runtime requirements.
- Monolithic re-exports from the primary package entry (rejected)
  Rejected because: Directly re-exporting from the primary bundle prevents modular tree-shaking and defeats the purpose of lightweight entry points.
  When valid: In environments where bundle footprint optimization is not a design requirement.

## Risks

- Breaking changes in the external core module unintentionally disrupt multiple downstream entry points simultaneously.
  Mitigation: Enforce contract verification tests across all modular export pathways in continuous integration.
  Owner: Library Architecture Team
- Transitive internal imports from the external module unintentionally bloat consumer bundles.
  Mitigation: Implement automated bundle size and export boundary analysis on pull requests modifying shared core modules.
  Owner: Library Architecture Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Ensure all re-exported symbols from the shared external core module preserve type definitions and parameter constraints identical to the primary library exports.
- Structure entry facades as pure re-export boundaries with minimal to zero runtime initialization code.

## Continuation Context


Verify commands:
- Discover the repository build script from the project manifest and execute the compilation verification task to validate module export compatibility.
- Locate the project test runner configuration and execute the suite targeting modular entry point exports.
- Query the workspace static analysis configuration and run the module import linter to verify that lightweight entry facades import exclusively from the canonical external core module.

Accept when:
- All lightweight entry facades successfully compile and resolve exports against the canonical external core module without unresolved references.
- Automated test suites confirm behavioral equivalence across all modular export pathways.
- Static analysis checks pass with zero reported violations of module boundary delegation rules.

## Enforcement

- Verified by: Automated continuous integration pipeline execution checking module export integrity and type signatures.
- Verified by: Peer code review validating that new entry facades delegate to the canonical external core module rather than duplicating runtime definitions.
- Verified by: Static analysis linting rules restricting direct internal cross-module dependencies.
- Violation handling: Pull requests introducing duplicate core implementations or bypassing the external core module are blocked from merging.
- Violation handling: Flagged architectural violations must be refactored to delegate directly to the canonical external core export.
- Exception process: Exceptions require written justification submitted via the architectural review workflow detailing why delegation is technically infeasible.
- Exception process: Approved exceptions must be time-bounded and documented within an architecture review record prior to code merge.