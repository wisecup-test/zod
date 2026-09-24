# Zod Core Library Module: Subsystem Decomposition Across Schemas, Checks, and Registries: Validation Issue Creation Error Formatting Reside

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- The Zod library core subsystem requires clear separation of validation responsibilities to prevent monolithic coupling among type schemas, check evaluators, error dispatchers, and runtime registries.
- Static analysis of the core library modules indicates recurring inter-module import relationships across schema definitions, check predicates, error generators, and parsing utilities.
- Centralized schema tracking and identity resolution are decoupled into dedicated registry abstractions rather than embedded directly inside individual schema instances.
- External schema interoperability demands standard schema protocol conformance without contaminating internal core validation mechanics.

## Problem Statement

A monolithic validation library design creates tight coupling between schema definitions, validation checks, error formatting, and runtime state management, impeding extensibility, increasing bundle overhead, and complicating cross-ecosystem schema interoperability.

## Decision

1. MUST: Validation issue creation and error formatting MUST reside within the dedicated error module and interface with check and schema execution via structured error callbacks.

## Policy Block

- MUST Validation issue creation and error formatting MUST reside within the dedicated error module and interface with check and schema execution via structured error callbacks.

In scope:
- Core library modules responsible for schema definition, parsing, validation checks, error dispatch, and schema registries.
- Internal cross-module references and interoperability contracts within the validation engine subsystem.

Out of scope:
- Third-party consumer applications that interact strictly with the public validation API.
- External standalone plugins or independent adapter libraries that do not touch the core module subsystem.

Exceptions:
- EXC-20-001: A performance-critical schema parsing hot path requires localized caching bypassing registry lookup.

## Rationale

- Partitioning the core validation engine into discrete modules isolates distinct concerns, allowing checks, parsing, errors, and schema representations to evolve independently.
- Centralizing schema instances and identity mappings inside a dedicated registry module provides controlled lifecycle management and avoids duplicate metadata accumulation across schemas.
- Standardizing schema interfaces allows external consumers and ecosystem tools to interact with validation schemas without coupling to internal engine implementation details.

## Consequences

Positive:
- High modularity allows independent testing, maintenance, and tree-shaking of individual core validation capabilities.
- Consistent error formatting and check execution across all schema primitives improves reliability.
- Encapsulated registry interfaces simplify schema introspection and metadata association.

Negative:
- Requires strict governance over module import hierarchies to prevent circular dependency cycles.
- Inter-module coordination introduces indirect call layers between schema invocation and low-level evaluation routines.

## Alternatives

- Monolithic Core Module (rejected)
  Rejected because: Consolidating all schemas, checks, errors, and registries into a single module results in high cognitive load, poor maintainability, and prevents granular tree-shaking.
  When valid: Valid only in minimal prototyping scenarios with fewer than five schema types.
- Class-Inheritance-Based Validation Engine (rejected)
  Rejected because: Heavy object-oriented hierarchies couple schema state to class prototypes, hindering functional composition and increasing runtime memory overhead.
  When valid: Valid in object-oriented framework ecosystems with rigid class reflection requirements.

## Risks

- Circular dependencies among core modules due to bidirectional references between schemas and parsing or check routines.
  Mitigation: Enforce unidirectional dependency boundaries through static analysis during continuous integration.
  Owner: engineering team
- Uncontrolled memory accumulation within global registry maps during long-running application runtimes.
  Mitigation: Provide explicit registry entry deletion methods and lifecycle management hooks.
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
- Maintain clear interface contracts between schema definition objects and the check execution subsystem to ensure check functions remain pure and stateless.
- Verify that all internal core module interactions reference abstract interfaces rather than private internal implementation details.

## Continuation Context


Verify commands:
- Discover and execute the repository dependency boundary verification script to ensure internal core module isolation.
- Discover and run the project test suite covering core schema execution, check validation, and registry caching.
- Discover and run the repository type-checking and linting workflows to verify interface adherence across all sub-modules.

Accept when:
- All core module unit and integration tests execute successfully without failure.
- Static analysis confirms zero circular dependencies between internal core library modules.
- Registry operations correctly store, retrieve, and delete schema instances without memory leakage.

## Enforcement

- Verified by: Automated continuous integration checks executing repository test suites and linting workflows.
- Verified by: Mandatory architectural peer review on pull requests modifying internal core module boundaries.
- Violation handling: Pull requests introducing circular dependencies or violating module encapsulation boundaries are blocked from merging.
- Violation handling: Code violating registry isolation or error handling contracts must be refactored before approval.
- Exception process: Submit an architectural review request detailing performance bottlenecks or runtime limitations requiring module boundary deviations.
- Exception process: Obtain explicit consensus from the repository core maintainers before merging an approved exception.