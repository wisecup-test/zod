---
version: 2
name: d6e6c217-ec1a-44ff-9d7f-65a2130ad2d8-valibot-schema-validation-adoption-validation-schemas-composed-independent-modular-schema
description: "Valibot Schema Validation Adoption: Validation Schemas Composed Independent Modular Schema"
metadata:
  actual:
    adr_id: d6e6c217-ec1a-44ff-9d7f-65a2130ad2d8
    status: accepted
    candidate_group_id: dc6286a1-b983-49d4-82ec-9f40035aa215
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Valibot Schema Validation Adoption: Validation Schemas Composed Independent Modular Schema

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/treeshake`

Applies to:
- `**` (whole root)

## Context

- The codebase requires runtime schema verification to ensure boundary data integrity while minimizing client bundle size.
- Static analysis identifies consistent modular adoption of Valibot across input validation schemas and tree-shakeable module boundaries.
- Standardizing on a modular schema validation library avoids inconsistent data parsing behaviors and bloated production artifacts across packages.

## Problem Statement

Inconsistent or heavyweight schema validation libraries introduce substantial bundle overhead and fragmented validation contracts across modules. The system requires a unified, lightweight, modular schema definition library that enforces runtime type safety without bundling unused validation routines.

## Decision

1. MUST: Validation schemas MUST be composed using independent modular schema functions rather than monolithic namespace objects to ensure dead-code elimination.

## Policy Block

- MUST Validation schemas MUST be composed using independent modular schema functions rather than monolithic namespace objects to ensure dead-code elimination.

In scope:
- Modules defining data schemas, input parsing, and runtime boundary validation.
- Components requiring modular schema verification and tree-shakeable packaging.

Out of scope:
- Internal language-primitive manipulations where formal schema boundaries are not exposed.
- Performance-critical inner loops where external schema parsing overhead is explicitly prohibited.

Exceptions:
- EXC-20-001: A third-party protocol requires a divergent schema validation specification

## Rationale

- Valibot provides modular, functional schema declarations that enable effective dead-code elimination, keeping bundle footprints minimal.
- Standardizing validation mechanics on a single modular library ensures uniform error handling and consistent type inference across repository modules.
- Evidence demonstrates multi-file adoption of Valibot across diverse schema primitives and structured objects.

## Consequences

Positive:
- Modular schema composition eliminates unused validation code from production bundles.
- Consistent runtime parsing contracts ensure predictable boundary data handling across modules.
- Static type inference is tightly coupled with runtime schema definitions, preventing type drift.

Negative:
- Functional schema composition syntax requires explicit imports for every validator and schema primitive.
- Upstream library API shifts across minor versions may require targeted schema refactoring.

## Alternatives

- Monolithic namespace-based schema validation libraries (rejected)
  Rejected because: Monolithic validation libraries import broad method namespaces that impair dead-code elimination and inflate bundle footprints.
  When valid: Environments where bundle size is negligible and legacy schema definitions predate modular validation adoption.
- Manual handwritten type guards and assertion functions (rejected)
  Rejected because: Handwritten validation lacks composability, introduces repetitive parsing logic, and risks divergence between runtime checks and static types.
  When valid: Isolated micro-utilities requiring zero external dependencies.

## Risks

- Accidental import of unnecessary validation utilities leading to unintended bundle size increases.
  Mitigation: Enforce modular import verification and bundle analysis in automated continuous integration checks.
  Owner: Architecture Team
- Schema version discrepancy between consuming modules and resolved library artifacts.
  Mitigation: Follow the Lock-Version Grounding policy to resolve and align exact library versions across manifests.
  Owner: Platform Engineering

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Import individual schema and validation primitives directly from the modular library namespace rather than re-exporting broad utility umbrellas.
- Derive static types directly from schema definitions using inferred type utilities to maintain synchronization between runtime constraints and compile-time types.

## Continuation Context


Verify commands:
- Discover the project test runner configuration from the repository manifest and execute the validation test suite.
- Discover the static analysis and type verification script from the repository manifest and run it to verify schema compilation.
- Discover the build bundle inspection script from repository configuration and execute it to verify modular tree-shaking compliance.

Accept when:
- All schema validation test suites execute and pass without validation or runtime errors.
- Static type checking completes with zero type errors for all inferred schema types.
- Bundle inspection confirms unused validation functions are eliminated from production output.

## Enforcement

- Verified by: Automated continuous integration pipeline running test suites and bundle size checks.
- Verified by: Static analysis and type checking during repository build verification.
- Verified by: Architecture and peer review on pull requests touching schema definitions.
- Violation handling: Pull requests introducing non-compliant validation libraries or unbundled namespace imports will fail continuous integration checks and be blocked from merging.
- Violation handling: Violations discovered in existing code must be logged as technical debt and refactored to standard modular schema patterns.
- Exception process: Submit an architectural deviation request documenting protocol constraints and performance justifications to the Architecture Review Board for formal evaluation.