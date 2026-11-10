---
version: 2
name: c797ae3b-6399-497d-9892-1ca5cc99966e-adoption-of-zod-for-runtime-schema-declaration-and-input-validation-data-structures-containing-multiple-fields-modeled
description: "Adoption of Zod for Runtime Schema Declaration and Input Validation: Data Structures Containing Multiple Fields Modeled"
metadata:
  actual:
    adr_id: c797ae3b-6399-497d-9892-1ca5cc99966e
    status: accepted
    candidate_group_id: 1a1e2218-cf8b-4cc0-bc62-7046d6a5fe5c
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Adoption of Zod for Runtime Schema Declaration and Input Validation: Data Structures Containing Multiple Fields Modeled

Status: proposed
Date: 2025-02-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/treeshake`

Applies to:
- `**` (whole root)

## Context

- The project requires consistent and reliable runtime data validation across modules handling structured inputs.
- Static type systems provide compile-time guarantees but do not protect execution environments from malformed runtime payloads.
- Multiple modules across the codebase independently require schema validation for primitive and composite data structures.

## Problem Statement

Without a unified runtime schema validation standard, data structures ingested from external or untrusted sources risk causing runtime type errors, inconsistent boundary handling, and duplicated manual validation logic across codebase modules.

## Decision

1. SHOULD: Data structures containing multiple fields SHOULD be modeled using object schema declarations composed of primitive validator types.

## Policy Block

- SHOULD Data structures containing multiple fields SHOULD be modeled using object schema declarations composed of primitive validator types.

In scope:
- All modules and packages defining data models that parse or ingest external or untrusted inputs.
- Internal boundaries requiring explicit schema contracts and runtime type validation.

Out of scope:
- Performance-critical inner loops where data has already passed boundary validation.
- Pure internal utility functions operating exclusively on compile-time verified primitives.

Exceptions:
- EXC-20-001: A module operates in an environment where schema parsing introduces unacceptable latency and inputs have been verified by an upstream gateway.

## Rationale

- Adopting Zod establishes a single declarative paradigm for authoring schemas and validating runtime payloads across packages.
- Zod enables direct schema composition with chained refinements and transformations, reducing custom validation boilerplate.
- Schema declarations provide dual utility by inferring static types while enforcing runtime integrity via parse operations.

## Consequences

Positive:
- Guarantees runtime data integrity at module ingestion points by rejecting invalid payloads early.
- Reduces redundant manual validation logic through reusable schema definitions.
- Synchronizes static type definitions with runtime validation logic through schema inference.

Negative:
- Introduces runtime execution latency during data parsing and schema validation.
- Increases bundle footprint due to the inclusion of runtime schema evaluation logic.

## Alternatives

- Manual imperative validation functions for each data structure (rejected)
  Rejected because: Imperative validation results in high maintenance overhead, inconsistent error reporting, and divergence between manual checks and static types.
  When valid: Valid in isolated scripts with no external dependencies and single primitive values.
- Pure compile-time type assertions without runtime validation (rejected)
  Rejected because: Compile-time assertions do not perform runtime checks, leaving applications vulnerable to malformed or unexpected data shapes.
  When valid: Valid only for closed internal systems where all producers and consumers share immutable memory space.

## Risks

- Schema parsing latency on large or deeply nested payloads may impact request throughput.
  Mitigation: Profile validation bottlenecks and structure schemas to parse only required boundary fields.
  Owner: Engineering Team
- Unsynchronized schema updates across package boundaries could reject valid evolving payloads.
  Mitigation: Maintain centralized or versioned schema definitions and test boundary parsing in automated test suites.
  Owner: Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Construct schemas modularly by defining reusable primitive validators and composing them into composite object schemas.
- Utilize refinement and transformation methods to enforce domain constraints such as string trimming and range limits directly within the schema pipeline.

## Continuation Context


Verify commands:
- Discover the repository script runner and execute the project verification test suite to ensure all schema validation tests pass.
- Discover the static analysis check defined in the project configuration and execute type checking to verify that schema inference aligns with declared data contracts.

Accept when:
- All discovered schema validation test suites execute and report zero failures.
- Static type analysis confirms that data types inferred from schemas match expected input contracts across all consumption boundaries.

## Enforcement

- Verified by: Automated test suites executing schema parsing validations during continuous integration.
- Verified by: Code review checks verifying that all external data ingress points apply schema parsing.
- Violation handling: Pull requests lacking schema validation at untrusted input boundaries will be blocked until compliant schemas and tests are added.
- Exception process: Exceptions must be submitted via architectural review with documented performance benchmarking and justification.