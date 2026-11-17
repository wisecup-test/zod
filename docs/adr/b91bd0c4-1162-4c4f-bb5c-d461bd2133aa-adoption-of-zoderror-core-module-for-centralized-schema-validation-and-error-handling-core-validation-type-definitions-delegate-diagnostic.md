---
version: 2
name: b91bd0c4-1162-4c4f-bb5c-d461bd2133aa-adoption-of-zoderror-core-module-for-centralized-schema-validation-and-error-handling-core-validation-type-definitions-delegate-diagnostic
description: "Adoption of ZodError Core Module for Centralized Schema Validation and Error Handling: Core Validation Type Definitions Delegate Diagnostic"
metadata:
  actual:
    adr_id: b91bd0c4-1162-4c4f-bb5c-d461bd2133aa
    status: accepted
    candidate_group_id: b1d967e1-d9ff-4665-b9a4-a3d48eb98cfa
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
---

# Adoption of ZodError Core Module for Centralized Schema Validation and Error Handling: Core Validation Type Definitions Delegate Diagnostic

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v3/**`

## Context

- Schema type definitions require unified error generation, type discrimination, and parsing validation without coupling individual type handlers directly to localization or error formatting implementations.
- Schema parsing workflows rely on standardized validation execution interfaces through methods such as parse and safeParse to return consistent issue collections.
- Modular separation between schema representation, parsing utilities, and the ZodError subsystem prevents cyclic coupling across type definitions and error formatting layers.

## Problem Statement

Scattering error construction, localized messaging, and validation diagnostics across independent schema type definitions leads to inconsistent issue formatting, duplicate parsing logic, and tightly coupled error hierarchies that complicate validation engine maintenance.

## Decision

1. MUST: Core validation type definitions MUST delegate all validation diagnostic emissions and issue formatting to the centralized ZodError module abstraction rather than constructing bespoke error objects.

## Policy Block

- MUST Core validation type definitions MUST delegate all validation diagnostic emissions and issue formatting to the centralized ZodError module abstraction rather than constructing bespoke error objects.

In scope:
- Core schema type definitions and parsing logic within the validation library package.
- Validation error generation, issue collection, and localized message formatting modules.

Out of scope:
- External consumer application logic that only ingests validated output without defining internal parsing routines.
- Standalone utility modules that operate without dependency on schema error structures.

## Rationale

- Evidence from the core validation modules demonstrates that type definitions delegate error handling to the dedicated ZodError module, preserving strict decoupling between type specification and diagnostic formatting.
- Standardizing validation execution through uniform parse and safeParse boundaries guarantees predictable error contracts across all supported schema checks.
- Isolating localization and parsing utility routines from schema definitions avoids circular dependencies and allows independent maintenance of localized error strings.

## Consequences

Positive:
- Centralized error handling through ZodError guarantees consistent diagnostic structures across all schema variations.
- Decoupling type declarations from error localization simplifies internationalization and error map customization.
- Uniform validation methods provide a predictable consumption contract for callers.

Negative:
- Schema type implementations must adhere to strict internal module boundaries rather than generating inline error messages.
- Internal delegation across multiple helper modules introduces layer indirection during validation error tracing.

## Alternatives

- Inline custom error generation within individual schema type definitions (rejected)
  Rejected because: Creating custom error structures within each schema type duplicates error formatting logic, produces inconsistent diagnostic shapes, and complicates global error mapping.
  When valid: Lightweight single-file validation scripts that have no external callers or localized message requirements.
- Throwing untyped primitive error strings upon validation failure (rejected)
  Rejected because: Untyped string errors lack structured issue paths, error codes, and metadata necessary for programmatic recovery and detailed user feedback.
  When valid: Minimal prototyping environments where structural error reporting is not required.

## Risks

- Inadvertent coupling between type definitions and concrete locale error maps could compromise module boundaries.
  Mitigation: Enforce module isolation boundaries so schema definitions interact only with abstract error utility interfaces rather than concrete locale files.
  Owner: Core Architecture Team
- Version drift between the resolved library version and internal API assumptions could cause unexpected runtime validation behavior.
  Mitigation: Adhere to the lock-version grounding process to verify the resolved library version against official documentation before implementation.
  Owner: Core Architecture Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Ensure all schema type evaluation logic routes through centralized error utilities rather than constructing direct error instances or formatting localized strings.
- Maintain distinct boundaries between parsing logic, discriminator resolution maps, and error emission to safeguard modularity and performance.

## Continuation Context


Verify commands:
- Discover the project's test execution script from the repository manifest and run the test suite to verify schema validation and error reporting behavior.
- Locate the repository typecheck script within the project manifest and run it to validate type compatibility across schema modules and error interfaces.
- Identify the static analysis script from the project configuration and execute it to ensure no prohibited cross-module references or unapproved error constructions exist.

Accept when:
- The project test suite passes completely with all schema validation and error handling scenarios verifying expected issue formats.
- The typecheck command completes with zero diagnostic errors across all schema type definitions and error utilities.
- Static analysis confirms strict compliance with module boundary rules and absence of inline error message formatting in schema types.

## Enforcement

- Verified by: Automated continuous integration pipeline executing repository test and typecheck scripts.
- Verified by: Peer code review verifying that schema types delegate to the centralized error subsystem and omit direct localization bindings.
- Violation handling: Pull requests introducing direct error formatting or bypassing centralized error utilities are rejected at code review.
- Violation handling: Build failures triggered by type mismatches or failing validation error tests block automated merging.
- Exception process: Exceptions for specialized low-overhead parsing utilities must be submitted via an architectural change request and approved by the core library maintainers.