# Zod Core Module Architecture: Centralized Error and Locale Foundation: Parsing Transformation Utilities Remain Stateless Helper

Status: proposed
Date: 2025-05-14
Deciders: Detection Pipeline (automated)

## Context

- The validation engine architecture requires consistent error representation, localized messaging, and shared utility execution across multiple runtime parsing helpers and public facades.
- Decentralized or duplicated error declarations across distinct helper subtrees create inconsistent error signatures, drift in localization formatting, and brittle exception handling for consumers.
- Centralizing foundational error constructs and localization mappings into a cohesive core module establishes a single source of truth for runtime validation behavior.
- Evidence indicates internal modules and parsing utilities consistently bind to centralized core primitives, error classes, and locale definitions.

## Problem Statement

Without a unified core module foundation, validation helper functions, parsing subroutines, and public facades risk declaring independent error structures, inconsistent localized error messaging, and redundant utility logic. This fragmentation leads to circular dependencies, diverging error payload formats, and increased maintenance overhead across the validation engine internal modules.

## Decision

1. SHOULD: Parsing and transformation utilities SHOULD remain stateless helper functions that accept input data and validation contexts while delegating issue accumulation and failure creation to core error constructs.

## Policy Block

- SHOULD Parsing and transformation utilities SHOULD remain stateless helper functions that accept input data and validation contexts while delegating issue accumulation and failure creation to core error constructs.

In scope:
- Internal library modules, parsing helper functions, and facade components within the validation engine requiring error modeling, localization, or core utility primitives.

Out of scope:
- External consumer application code importing only the root public API entry points.
- Standalone utility scripts that do not interact with validation runtime execution or error reporting.

## Rationale

- Centralizing foundational error structures, such as ZodError, and localization definitions within a dedicated core module ensures uniform validation error output across all parsing helpers.
- Enforcing unidirectional dependencies from parsing helpers to the core module prevents circular reference deadlocks and simplifies runtime compilation.
- Consolidating locale definitions within the core architecture allows global error message customization without requiring modification to distributed parsing logic.

## Consequences

Positive:
- Guarantees consistent error formats and localization handling across all schema parsing subroutines.
- Eliminates circular dependencies between public facades, parsing helpers, and foundational error models.
- Simplifies maintenance by providing a single canonical module for foundational validation utilities and error prototypes.

Negative:
- Requires all internal helper modules to adhere strictly to the core module contract, preventing isolated ad-hoc error structures.
- Changes to core error contracts require synchronized updates and regression verification across all dependent parsing subsystems.

## Alternatives

- Localized error definitions and helper utilities co-located within individual parsing subdirectories (rejected)
  Rejected because: Leads to code duplication, diverging error payloads, inconsistent localization behavior, and tight coupling between isolated helpers.
  When valid: Small, single-file validation scripts where modular decomposition introduces unnecessary indirection.
- Adoption of a centralized core module housing error types, locale bindings, and foundational utilities (accepted)
  Rejected because: Not applicable; this option satisfies architectural decoupling and uniformity requirements.
  When valid: Modular libraries requiring consistent error contracts, localized formatting, and reusable runtime validation helpers.

## Risks

- Core module expansion into a monolithic shared module containing unrelated domain logic
  Mitigation: Restrict core module contents strictly to foundational primitives, standard error classes, and base localization definitions through architectural boundary checks.
  Owner: engineering team
- Inadvertent introduction of backward dependencies from core modules to higher-level parsing helpers
  Mitigation: Enforce unidirectional dependency rules using continuous integration static analysis and type checks.
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
- Discover the centralized core exports and ensure new parsing helpers consume shared error classes and locale definitions through the established core module boundary.
- Maintain unidirectional architecture by verifying that the core module boundary has zero references to specialized schema types or peripheral runtime helpers.

## Continuation Context


Verify commands:
- Discover the project script definitions and execute the repository type-checking suite to verify module boundary compliance.
- Discover and run the project test execution runner to ensure error generation and localization resolution pass all suite checks.
- Discover the repository static analysis and linting scripts to verify import directionality and module dependency constraints.

Accept when:
- The discovered type verification and test execution suites pass with zero errors across all core module consumers.
- Import analysis confirms all schema parsing and helper modules import error types and locale definitions strictly from the designated core module boundary.
- No circular dependencies exist between core foundation modules and downstream helper or facade modules.

## Enforcement

- Verified by: Automated type checking and architectural boundary analysis during continuous integration workflows.
- Verified by: Peer code review confirming adherence to core module import conventions.
- Violation handling: Pull requests introducing circular dependencies, locally duplicated error structures, or bypassed core locale maps are blocked from merging.
- Violation handling: Violations identified during code review require refactoring to route dependencies through the centralized core module.
- Exception process: Exceptions require an architectural review proposal demonstrating technical necessity when core exports cannot satisfy specialized parsing requirements.
- Exception process: Approved exceptions must be documented in the repository architecture tracking documentation with an associated migration plan.