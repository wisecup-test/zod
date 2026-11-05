---
version: 2
name: 16be4ea5-22ca-4902-a7df-d2b65ae63bbb-adoption-of-zod-mini-for-modular-schema-definition-and-input-validation-modules-requiring-schema-definition-runtime-input
description: "Adoption of zod/mini for Modular Schema Definition and Input Validation: Modules Requiring Schema Definition Runtime Input"
metadata:
  actual:
    adr_id: 16be4ea5-22ca-4902-a7df-d2b65ae63bbb
    status: accepted
    candidate_group_id: 6019c7a4-9a84-4a99-a2a2-7b9ec4210fe7
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/bench/**
      - packages/resolution/src/**
      - packages/treeshake/**
---

# Adoption of zod/mini for Modular Schema Definition and Input Validation: Modules Requiring Schema Definition Runtime Input

Status: proposed
Date: 2025-05-15
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `packages/bench/**`
- `packages/resolution/src/**`
- `packages/treeshake/**`

## Context

- Runtime input validation and data structure parsing are required across multiple packages and target distribution formats.
- Monolithic schema validation imports introduce unnecessary bundle overhead in tree-shakeable client and utility modules.
- Multiple modules standardize on modular schema primitives to combine declarative type validation with minimal footprint.

## Problem Statement

Adopting monolithic schema validation libraries causes excessive bundle size and dead-code retention across modular packages, requiring an architectural constraint to adopt modular, tree-shakeable validation primitives.

## Decision

1. MUST: Modules requiring schema definition and runtime input validation MUST import and utilize the zod/mini entry point.

## Policy Block

- MUST Modules requiring schema definition and runtime input validation MUST import and utilize the zod/mini entry point.

In scope:
- All runtime input parsing, schema definitions, and payload verification in shared and client-facing packages.

Out of scope:
- Internal utility functions that operate strictly on pre-validated, strongly typed memory structures.

## Rationale

- Evidence across multiple packages demonstrates consistent utilization of modular schema primitives and parsing methods for input validation.
- Using modular validation entry points enforces uniform schema semantics while preserving optimal dead-code elimination across diverse module resolution formats.

## Consequences

Positive:
- Reduces bundle payload and improves dead-code elimination by importing modular validation primitives.
- Standardizes runtime input parsing and schema verification across diverse module distribution targets.
- Provides declarative data structure parsing with explicit check combinators.

Negative:
- Developers must explicitly compose validation constraints rather than relying on auto-chained monolithic helper methods.
- Schema composition requires strict adherence to modular check functions to prevent accidental inclusion of unneeded parsing logic.

## Alternatives

- Adopting a full monolithic validation export namespace across all validation modules (rejected)
  Rejected because: Importing monolithic validation namespaces prevents granular dead-code elimination and increases runtime bundle overhead across lightweight entry points.
  When valid: Valid when building isolated server-side environments where deployment bundle size is unconstrained.
- Manual type-narrowing predicates without centralized schema definitions (rejected)
  Rejected because: Manual assertions lack declarative schema composition and fail to provide unified runtime parsing with structured error reporting.
  When valid: Valid when runtime validation requirements are limited to primitive checks with zero third-party module tolerance.

## Risks

- Inconsistent schema composition across teams due to unfamiliarity with modular check pipelines.
  Mitigation: Establish shared schema utilities and documentation for modular check composition.
  Owner: engineering team
- Accidental import of monolithic validation entry points re-introducing bundle bloat.
  Mitigation: Enforce import rules in static analysis to prevent importing full root validation entry points.
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
- Compose complex validations by piping modular checks into base schemas rather than importing monolithic utility suites.
- Ensure all schema parsing logic handles failure states uniformly at runtime boundaries.

## Continuation Context


Verify commands:
- Discover and run the repository verification scripts that validate module imports and runtime parsing test suites.
- Inspect module resolution outputs to verify that only modular validation primitives are bundled into target artifacts.

Accept when:
- All schema validation implementations execute runtime parsing through the designated modular validation entry point.
- Repository verification scripts confirm schema validation tests pass without unapproved monolithic validator imports.

## Enforcement

- Verified by: Automated static analysis and module import inspection in continuous integration workflows.
- Verified by: Code review verification of schema definition patterns and parsing calls.
- Violation handling: Flag imports of non-modular validation namespaces as blocking lint or static analysis violations.
- Violation handling: Require refactoring of direct manual validation assertions into standardized modular schema definitions.
- Exception process: Submit an architectural review request documenting technical constraints that necessitate alternative schema validation mechanisms.
- Exception process: Obtain sign-off from module owners prior to introducing external schema parsers.