---
version: 2
name: 830ff52d-3f73-4985-85e3-fcd647bbd1a5-zoderror-centralized-validation-error-representation-architecture-parsing-helper-routines-delegate-error-issue
description: "ZodError Centralized Validation Error Representation Architecture: Parsing Helper Routines Delegate Error Issue"
metadata:
  actual:
    adr_id: 830ff52d-3f73-4985-85e3-fcd647bbd1a5
    status: accepted
    candidate_group_id: 2a760602-eb59-42b6-93ff-193614615ecc
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
---

# ZodError Centralized Validation Error Representation Architecture: Parsing Helper Routines Delegate Error Issue

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v3/**`

## Context

- Schema validation systems require consistent error reporting structures across diverse data types and parsing routines.
- Separation of concerns requires decoupling core parsing mechanics from locale-specific error string synthesis.
- Parsing utilities and error localization formatters must adhere to a single unified contract for validation issues and shared helpers.

## Problem Statement

Without a centralized validation error representation and shared utility convention, parsing routines risk generating disparate error shapes, duplicating helper routines, and entangling localized human-readable messages directly with parsing logic.

## Decision

1. MUST: Parsing helper routines MUST delegate error issue construction to centralized error utility functions rather than instantiating ad-hoc error shapes.

## Policy Block

- MUST Parsing helper routines MUST delegate error issue construction to centralized error utility functions rather than instantiating ad-hoc error shapes.

In scope:
- Schema parsing and validation execution pipelines.
- Validation error message localization and formatting modules.
- Core error representation and issue construction helper modules.

Out of scope:
- External schema consumer applications consuming final instantiated error instances.
- Standalone third-party plugins that do not participate in internal parsing issue construction or localization.

## Rationale

- Adopting ZodError as the unified error representation establishes a consistent contract for issue reporting across all schema validators.
- Routing error generation through common utility helpers prevents fragmentation of error handling behavior and simplifies maintenance.
- Isolating locale definitions from parser internals allows dynamic language translation without modifying parsing algorithms.

## Consequences

Positive:
- Ensures uniform error issue structures and diagnostic metadata across all schema parsing routines.
- Decouples parsing mechanics from specific human-readable message strings, facilitating independent localization.
- Centralizes validation issue formatting logic in shared utilities to prevent logic duplication.

Negative:
- Internal helper and localization modules incur direct structural coupling to the central ZodError schema definitions.
- Changes to error issue data structures require synchronized updates across parsing utilities and localization mappings.

## Alternatives

- Decentralized Ad-Hoc Error Structures (rejected)
  Rejected because: Constructing error payloads independently inside individual parsing utilities causes inconsistent error shapes, duplicated formatting logic, and brittle localization contracts.
  When valid: Isolated single-file scripts or experimental prototype parsers without multi-locale requirements.
- Inline String-Only Error Message Generation (rejected)
  Rejected because: Synthesizing localized error strings directly during parsing tightly couples validation mechanics to specific language strings, preventing structured programmatic error introspection and dynamic localization.
  When valid: Lightweight validation runtimes where structured error metadata is unnecessary and bundle size is the primary constraint.

## Risks

- Circular dependency cycles between parsing utilities, error definitions, and localization formatters.
  Mitigation: Maintain strict module layering where error definitions and common utilities serve as leaf dependencies imported by parsers and locales without back-references.
  Owner: Core Engineering Team
- Breaking modifications to ZodError issue schemas destabilizing downstream consumers and locale formatters.
  Mitigation: Enforce comprehensive regression test suites covering all issue types and maintain stable interface contracts for issue descriptors.
  Owner: Core Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Shared utility modules must contain side-effect-free helper routines to ensure safe consumption across both parsing and localization layers.
- Localization formatters must consume structured issue descriptors rather than raw parser internal state to maintain loose coupling.

## Continuation Context


Verify commands:
- Discover the test runner defined in the project configuration manifest and execute the test suite covering parsing utilities and error localization.
- Discover the static analysis and type checking script configured in the project repository and run it to verify module import resolution and type consistency across core error modules.
- Inspect the project dependency resolution artifact to confirm all module imports align with declared dependency boundaries.

Accept when:
- All schema parsing and localization test suites pass without validation issue schema mismatches.
- Automated static type verification passes with zero type errors across module boundaries consuming ZodError and shared utility functions.
- Validation error emissions consistently conform to the standardized issue descriptors defined by ZodError across all configured locales.

## Enforcement

- Verified by: Automated static type analysis verifying that all error constructions adhere to ZodError type definitions.
- Verified by: Continuous integration test suites verifying issue formatting and locale message generation across parsing routines.
- Verified by: Peer code review verifying that new parsing utilities do not introduce ad-hoc error structures.
- Violation handling: Pull requests introducing unstandardized error shapes or bypassing centralized error utilities are rejected.
- Violation handling: Static analysis failures on incompatible error issue structures block integration pipelines.
- Exception process: Exceptions to centralized error issue representation require architectural review and formal approval by the core maintainers.
- Exception process: Any approved deviation must be accompanied by dedicated regression tests verifying compatibility with standard error handling consumers.