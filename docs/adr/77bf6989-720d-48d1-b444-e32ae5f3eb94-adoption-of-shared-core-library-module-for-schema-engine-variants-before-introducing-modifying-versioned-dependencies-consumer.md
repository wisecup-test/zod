---
version: 2
name: 77bf6989-720d-48d1-b444-e32ae5f3eb94-adoption-of-shared-core-library-module-for-schema-engine-variants-before-introducing-modifying-versioned-dependencies-consumer
description: "Adoption of Shared Core Library Module for Schema Engine Variants: Before Introducing Modifying Versioned Dependencies Consumer"
metadata:
  actual:
    adr_id: 77bf6989-720d-48d1-b444-e32ae5f3eb94
    status: accepted
    candidate_group_id: 138011fb-83e8-4014-9ddd-f54efb32a93b
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Adoption of Shared Core Library Module for Schema Engine Variants: Before Introducing Modifying Versioned Dependencies Consumer

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v4/**`

## Context

- Multiple schema engine variants require identical baseline parsing logic, standard validation rules, and regular expressions.
- Independent re-implementation of parsing and registry routines across engine variants increases maintenance overhead and introduces behavioral divergence.
- Centralizing core execution utilities and global registry operations into an internal shared core module enables consistent schema introspection and execution behavior.

## Problem Statement

Maintaining parallel schema engine variants without a centralized foundation creates duplicated validation logic, inconsistent registry handling, and divergent schema processing behaviors across different engine targets.

## Decision

1. MUST: Before introducing or modifying versioned dependencies, the consumer MUST inspect the repository lock or resolution artifact to verify the exact resolved dependency version.

## Policy Block

- MUST Before introducing or modifying versioned dependencies, the consumer MUST inspect the repository lock or resolution artifact to verify the exact resolved dependency version.

In scope:
- Schema engine variant definitions requiring shared parsing, registry lookup, or validation logic.
- Modules implementing schema validation contracts and instance registries.

Out of scope:
- Standalone utility functions that operate independently of schema parsing and registry state.
- External adapters that interact with schema engines solely through public validation interfaces.

## Rationale

- Centralizing primitives in the core library module guarantees identical regular expression matching and validation behavior across all schema variants.
- Utilizing core.globalRegistry ensures that schema metadata and instances remain discoverable across independent variant boundaries.
- Segregating core parsing mechanisms from variant surface APIs simplifies long-term maintenance and prevents divergent behavior.

## Consequences

Positive:
- Ensures uniform schema parsing and regular expression evaluation across all engine variants.
- Eliminates duplicate parsing and registry management logic across implementations.
- Establishes a centralized boundary for schema registration and inspection through core.globalRegistry.

Negative:
- Tightly couples schema engine variants to the internal API contract of the core module.
- Modifications to core validation routines require coordinated regression testing across all dependent schema variants.

## Alternatives

- Decentralized schema implementations where each engine variant maintains local validation checks and regular expression definitions (rejected)
  Rejected because: Creates divergent parsing behavior and high duplicate maintenance overhead across schema variants
  When valid: When schema variants share no execution primitives or cross-compatibility requirements
- Monolithic schema engine without engine variant segregation (rejected)
  Rejected because: Prevents the deployment of lightweight execution profiles for resource-constrained runtime environments
  When valid: When a single universal execution profile satisfies all consumer performance requirements

## Risks

- Breaking changes in core module interfaces may cascade and disrupt dependent schema variants
  Mitigation: Enforce comprehensive contract test suites against all variants before publishing core module changes
  Owner: engineering team
- Global registry state collisions when multiple schema variants register overlapping identifiers
  Mitigation: Enforce strict schema registration naming and lookup isolation mechanisms within core.globalRegistry
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
- Schema variant implementations must verify that interactions with core.globalRegistry properly handle type casting and instance retrieval across execution contexts.
- When extending schema parsing capabilities, developers must evaluate whether new validation checks belong in the shared core module or variant-specific extensions.

## Continuation Context


Verify commands:
- Discover and run the project static analysis and linting scripts to verify adherence to module import boundaries.
- Discover and execute the project test runner across all schema variant test suites to ensure uniform validation behavior.
- Inspect dependency manifests and resolution artifacts to confirm that dependency version declarations match lock state.

Accept when:
- All schema variant test suites pass without regressions across validation parsing and execution.
- Static boundary verification confirms schema modules import shared parsing and registry primitives exclusively from the internal core module.
- Registry lookup tests confirm consistent resolution of schema instances through core.globalRegistry across variants.

## Enforcement

- Verified by: Continuous integration automated test suites
- Verified by: Static module dependency analysis and import boundary linters
- Verified by: Peer code reviews on all schema engine pull requests
- Violation handling: Pull requests that duplicate core parsing logic or bypass the shared core module are blocked from merging.
- Violation handling: Violations discovered in active development must be refactored to consume shared core primitives before acceptance.
- Exception process: Exceptions require documented architectural justification demonstrating why a specialized schema variant cannot utilize the shared core module, approved by the lead architect.