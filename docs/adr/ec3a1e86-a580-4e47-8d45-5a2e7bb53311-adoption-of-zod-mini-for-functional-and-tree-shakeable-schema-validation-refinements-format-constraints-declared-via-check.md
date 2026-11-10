---
version: 2
name: ec3a1e86-a580-4e47-8d45-5a2e7bb53311-adoption-of-zod-mini-for-functional-and-tree-shakeable-schema-validation-refinements-format-constraints-declared-via-check
description: "Adoption of zod/mini for Functional and Tree-Shakeable Schema Validation: Refinements Format Constraints Declared Via Check"
metadata:
  actual:
    adr_id: ec3a1e86-a580-4e47-8d45-5a2e7bb53311
    status: accepted
    candidate_group_id: 4ecfb3a9-b029-42f8-9301-7d71eb684470
    evidence:
      source: deep
  scope:
    root: packages/treeshake
---

# Adoption of zod/mini for Functional and Tree-Shakeable Schema Validation: Refinements Format Constraints Declared Via Check

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/treeshake`

Applies to:
- `**` (whole root)

## Context

- Application boundaries and data transformation pipelines require rigorous runtime schema validation to ensure input integrity.
- Monolithic validation library imports bundle unused validators and schema types, increasing distribution size.
- Adopting a modular, functional entrypoint isolates specific validator imports to only those required by each schema.

## Problem Statement

Runtime data validation across distributed application boundaries requires a uniform schema definition mechanism, but monolithic validator packages introduce substantial dead-code overhead in production distributions.

## Decision

1. SHOULD: Refinements and format constraints SHOULD be declared via the check method using discrete validator functions including minLength, maxLength, email, trim, and refine.

## Policy Block

- SHOULD Refinements and format constraints SHOULD be declared via the check method using discrete validator functions including minLength, maxLength, email, trim, and refine.

In scope:
- Input validation layers and data parsing modules across the codebase.
- Runtime schema definitions for structured and primitive payload verification.

Out of scope:
- Static type assertions that do not require runtime data boundary validation.
- Legacy subsystems with dedicated isolated validator implementations.

## Rationale

- The IR evidence confirms adoption of the zod/mini functional entrypoint across multiple schema declarations.
- Discrete validation checks such as minLength, maxLength, email, and trim are composed via the check method, preserving tree-shakeability.
- Adopting modular entrypoints maintains runtime validation guarantees while optimizing bundle efficiency.

## Consequences

Positive:
- Reduces bundle footprint by enabling dead-code elimination of unused schema validators and constraints.
- Provides explicit, composable validation pipelines using discrete check functions.
- Ensures consistent runtime boundary data parsing and static type inference.

Negative:
- Requires developers to adapt to discrete check composition functions rather than monolithic prototype method chaining.
- Increases import statement granularity across files defining diverse validation constraints.

## Alternatives

- Standard Monolithic Schema Validation Entrypoint (rejected)
  Rejected because: Includes all schema types and validator methods in the bundle regardless of whether they are utilized, inflating bundle size.
  When valid: Valid when bundle size is not a constraint and monolithic method chaining across all schema types is required.
- Custom Ad-Hoc Runtime Assertion Functions (rejected)
  Rejected because: Lacks unified schema declarations, automated type inference, and centralized error handling for structural payloads.
  When valid: Valid for isolated low-level primitives where external library dependencies are prohibited.

## Risks

- Inadvertent importation of monolithic validator modules bypassing tree-shakeable packaging.
  Mitigation: Configure static analysis import restrictions and module boundary enforcement rules.
  Owner: Engineering Team
- API surface divergence between modular functional checks and standard chaining syntax.
  Mitigation: Provide standardized validation schema templates and developer documentation across the repository.
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
- Declare object structures using z.object with discrete primitive fields and attach validation rules via the check method to ensure individual validator functions remain tree-shakeable.
- Centralize schema definitions adjacent to data transfer contracts or boundary ingress points to ensure consistent parsing execution across consumers.

## Continuation Context


Verify commands:
- Discover the project dependency manifest and lock file to inspect the declared and resolved module entries for the schema validation library.
- Execute the project automated test suite via the repository script runner to validate schema parsing assertions.
- Run the project static type checker and linter to ensure all schema definitions adhere to functional entrypoint constraints.

Accept when:
- All schema validation invocations resolve through the modular functional entrypoint without importing monolithic packages.
- Input parsing tests successfully verify structural and constraint assertions using schema parse methods.
- Static analysis and type checking pass without errors across all modules declaring validation schemas.

## Enforcement

- Verified by: Automated test suites asserting runtime schema validation and rejection behavior.
- Verified by: Static analysis import rules verifying that schema imports use the functional entrypoint.
- Verified by: Peer code review for new schema definitions and boundary validation logic.
- Violation handling: Pull requests importing non-modular entrypoints are blocked by static analysis checks.
- Violation handling: Unvalidated data inputs at system boundaries trigger test failures requiring schema enforcement.
- Exception process: Exceptions require documented justification demonstrating why modular schema validation cannot satisfy runtime constraints, approved by architecture review.