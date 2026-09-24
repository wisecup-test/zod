# Valibot Modular Schema Validation Adoption: Schemas Not Bypass Runtime Validation When

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- The codebase validates runtime inputs and structured payloads across execution contexts and performance-critical boundaries.
- Benchmark and tree-shake verification suites evaluate schema validation dependencies to ensure minimal bundle overhead and efficient modular inclusion.
- Valibot is integrated across multiple modules to provide functional, composable schema definitions that support aggressive dead-code elimination.

## Problem Statement

Runtime data validation frequently introduces substantial bundle overhead when monolithic schema libraries are used. The project requires a modular, tree-shakeable validation library that allows applications to import only the validation functions strictly necessary for each schema, without bundling unused validation code or runtime utilities.

## Decision

1. MUST_NOT: Schemas MUST NOT bypass runtime validation when parsing untrusted external inputs across public API boundaries.

## Policy Block

- MUST_NOT Schemas MUST NOT bypass runtime validation when parsing untrusted external inputs across public API boundaries.

In scope:
- Runtime input parsing, structured schema definition, and payload validation across application modules.
- Performance-sensitive and bundle-constrained packages where tree-shaking and dead-code elimination are required.

Out of scope:
- Internal-only modules where compile-time static type checking is sufficient without runtime boundaries.
- Isolated comparative benchmark implementations reserved for historical evaluation.

Exceptions:
- EXC-20-001: A specialized domain component requires legacy schema definitions during incremental migration.

## Rationale

- Valibot provides a functional, modular architecture where every validator and schema constructor is an independent export, minimizing production bundle impact.
- Adopting a tree-shakeable schema validation mechanism ensures consistent runtime validation guarantees while preventing monolithic validation bundle bloat.
- Evidence across benchmark and verification suites demonstrates consistent integration of Valibot schema definitions for primitive and structured validation.

## Consequences

Positive:
- Significantly reduced bundle footprint through functional decomposition and dead-code elimination of unused schema validators.
- Strict runtime input validation coupled with static type inference derived directly from declarative schemas.
- Standardized schema declaration patterns across application packages and boundary layers.

Negative:
- Functional composition syntax requires adaptation for engineers accustomed to fluent, chained-method schema builder interfaces.
- Granular import management is required to avoid importing monolithic entry points that undermine tree-shaking gains.

## Alternatives

- Monolithic chained-API schema validation library (rejected)
  Rejected because: Monolithic schema validation libraries bundle unused parsing and transformation logic, increasing production client payload sizes.
  When valid: When bundle size is not a factor and fluent method-chaining syntax is strictly mandated.
- Compile-time only type checking without runtime validation (rejected)
  Rejected because: Omitting runtime validation exposes boundary interfaces to unverified external inputs and runtime type inconsistencies.
  When valid: When input data sources are strictly verified by isolated upstream boundaries.

## Risks

- Developers may inadvertently import large helper utilities rather than granular validation primitives, impacting bundle optimization.
  Mitigation: Enforce granular import linting rules and verify bundle output metrics in continuous integration.
  Owner: Engineering Team
- Rapid evolution of functional validation APIs may require version-specific schema adaptations.
  Mitigation: Follow the mandatory lock-version grounding policy to match schema declarations against authoritative resolved library documentation.
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
- Construct schemas using modular functional composition, importing only the specific validators and types required for each payload.
- Verify tree-shaking metrics during module bundling to ensure dead-code elimination operates effectively on schema definitions.

## Continuation Context


Verify commands:
- Discover the project test runner from the dependency manifest and execute the test suite to verify schema validation compliance.
- Discover and run the project build script to confirm that tree-shaking and bundle generation succeed without unresolved validation imports.

Accept when:
- All schema validation tests pass across packages importing the validation library.
- Production bundle analysis confirms that only imported validation primitives are included in target distribution artifacts.

## Enforcement

- Verified by: Automated continuous integration checks executing test suites and bundle size analyzers.
- Verified by: Peer code reviews verifying modular import practices and schema boundary definitions.
- Violation handling: Pull requests introducing monolithic validation workarounds or unvalidated boundary inputs will fail automated checks and require remediation before merge.
- Exception process: Submit an architectural deviation request detailing rationale, impact analysis, and an incremental migration plan to the architecture review team.