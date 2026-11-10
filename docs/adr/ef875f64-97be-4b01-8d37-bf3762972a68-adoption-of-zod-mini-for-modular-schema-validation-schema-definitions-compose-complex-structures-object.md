---
version: 2
name: ef875f64-97be-4b01-8d37-bf3762972a68-adoption-of-zod-mini-for-modular-schema-validation-schema-definitions-compose-complex-structures-object
description: "Adoption of @zod/mini for Modular Schema Validation: Schema Definitions Compose Complex Structures Object"
metadata:
  actual:
    adr_id: ef875f64-97be-4b01-8d37-bf3762972a68
    status: accepted
    candidate_group_id: 19ba1074-3608-4fc6-9490-5ff43e413b98
    evidence:
      source: deep
  scope:
    root: packages/integration
    paths:
      - fixtures/internal-types/**
---

# Adoption of @zod/mini for Modular Schema Validation: Schema Definitions Compose Complex Structures Object

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/integration`

Applies to:
- `fixtures/internal-types/**`

## Context

- Schema validation requires consistent structure across modules and dual runtime environments without introducing unnecessary library overhead.
- The project integrates @zod/mini to construct composable validation schemas for objects, primitives, enums, arrays, and records.
- Both ECMAScript and CommonJS module formats require uniform validation contracts and schema definition APIs.

## Problem Statement

Validating runtime data structures across diverse execution targets requires consistent type enforcement without incurring heavy bundle size penalties or multi-runtime incompatibilities from full-featured schema validation suites.

## Decision

1. MUST: Schema definitions MUST compose complex structures using z.object and z.record builders with explicitly typed property schemas.

## Policy Block

- MUST Schema definitions MUST compose complex structures using z.object and z.record builders with explicitly typed property schemas.

In scope:
- Modules defining runtime schema validation contracts, data transfer object validation, or type integrity boundaries.
- Internal types and integration testing fixtures verifying dual module runtime compatibility.

Out of scope:
- Third-party interface definitions that do not participate in runtime schema parsing or data assertion.
- Components with specialized domain-specific binary serialization layers that do not parse structured object payloads.

## Rationale

- @zod/mini provides a streamlined functional schema validation footprint while maintaining strict runtime parsing semantics.
- Utilizing chained validation checks and modular builder functions preserves type safety without loading monolithic validation bundles.
- Dual module compatibility ensures uniform schema evaluation across both ECMAScript and CommonJS consumption contexts.

## Consequences

Positive:
- Reduced bundle and runtime overhead through minimal schema definitions.
- Predictable and uniform validation behavior across dual module formats.
- Clear and composable schema syntax using modular validation checks.

Negative:
- Advanced transformations and third-party plugins available only in monolithic validation libraries require custom implementations.
- Schema authors must explicitly compose constraints using modular check methods rather than relying on bundled convenience helpers.

## Alternatives

- Standardizing on the full monolithic validation package (rejected)
  Rejected because: The full library introduces unnecessary bundle weight and feature overhead for lightweight validation contexts where modular checks suffice.
  When valid: Valid when complex nested schemas require extensive built-in transformations and third-party plugin integrations that cannot be represented minimally.
- Manual runtime type guards and custom validation assertions (rejected)
  Rejected because: Manual type guards introduce duplicate maintenance effort, drift from static type signatures, and lack centralized error reporting.
  When valid: Valid in performance-critical hot paths where function call overhead of schema parsing cannot be tolerated.

## Risks

- Divergence between schema definition capabilities in the mini variant versus full schema libraries leading to unsupported validation constructs.
  Mitigation: Validate all required schema methods against the locked library documentation and encapsulate custom validators using modular check functions.
  Owner: engineering team
- Inconsistent behavior between dual module evaluation contexts during schema execution.
  Mitigation: Maintain automated integration tests exercising schema evaluation under both module resolution formats.
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
- Construct schema definitions by importing modular builder functions and composing validation constraints sequentially.
- Verify dual module resolution compatibility by structuring exports to satisfy both ECMAScript and CommonJS import mechanisms.

## Continuation Context


Verify commands:
- Discover and run the project test execution script to evaluate schema validation suite passes.
- Discover and run the project type check script to ensure static type inference aligns with runtime schemas.
- Discover and run the project module build verification script across all supported module targets.

Accept when:
- All schema validation test fixtures execute without parsing errors under both ECMAScript and CommonJS module formats.
- Static type checking completes with zero diagnostic errors across all schema definitions and inferred types.

## Enforcement

- Verified by: Automated continuous integration pipeline running test suites and type verification.
- Verified by: Peer code review confirming adherence to modular schema builder patterns.
- Violation handling: Pull requests introducing monolithic validation library imports or unconstrained schemas are blocked until aligned with modular validation standards.
- Exception process: Submit an architectural deviation request detailing specific schema capabilities unavailable in the mini variant, subject to engineering lead approval.