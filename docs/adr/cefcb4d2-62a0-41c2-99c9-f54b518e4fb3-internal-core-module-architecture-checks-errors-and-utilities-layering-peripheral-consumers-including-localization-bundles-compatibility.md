# Internal Core Module Architecture: Checks, Errors, and Utilities Layering: Peripheral Consumers Including Localization Bundles Compatibility

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Peripheral modules such as localization bundles and backward-compatibility layers require access to common error definitions, assertion checks, and utility primitives.
- Monolithic entry points or barrel imports introduce circular dependency risks and inflate bundle sizes when peripheral consumers only require foundational primitives.
- Establishing internal core submodule boundaries allows modular consumption of checks, errors, and utilities across distinct localization and compatibility components.

## Problem Statement

Peripheral library extensions, internationalization dictionaries, and backward-compatibility adapters frequently require core validation error structures and assertion logic. Importing these structures from unified library entry points risks circular dependencies, tree-shaking failures, and unnecessary compilation bloat in consumers that only need low-level check, error, or utility contracts.

## Decision

1. MUST: Peripheral consumers including localization bundles and compatibility adapters MUST import foundational validation checks, error representations, and utility helpers directly from dedicated internal core submodules rather than monolithic barrel exports.

## Policy Block

- MUST Peripheral consumers including localization bundles and compatibility adapters MUST import foundational validation checks, error representations, and utility helpers directly from dedicated internal core submodules rather than monolithic barrel exports.

In scope:
- Localization dictionary modules providing translated error maps and validation messages
- Compatibility adapters maintaining legacy API surfaces against internal core contracts
- Internal submodules requiring direct access to core checks, errors, or utility functions

Out of scope:
- Public top-level consumer applications consuming published external package entry points
- Self-contained utility modules with no dependency on validation errors or check primitives

## Rationale

- Direct consumption of dedicated core submodules prevents circular dependency graphs between core validation engines and localization error dictionaries.
- Isolating checks, errors, and utility primitives allows individual localization bundles to remain minimal in footprint, including only the specific runtime dependencies required for message mapping.
- Standardizing import boundaries across peripheral modules ensures consistent error formatting and check resolution without coupling to concrete schema implementations.

## Consequences

Positive:
- Eliminates circular dependency cycles between localization dictionaries and top-level schema definitions.
- Optimizes modular bundle sizes and dead-code elimination by preventing accidental imports of unnecessary core machinery.
- Decouples error message definitions from validation runtime logic, enabling independent maintenance and scaling of locale collections.

Negative:
- Increases the surface area of internal module contracts that must remain stable across internal refactoring.
- Requires strict enforcement of subpath import boundaries across all peripheral modules to avoid regression into barrel imports.

## Alternatives

- Monolithic Barrel Import via Single Internal Entry Point (rejected)
  Rejected because: Importing all core functions through a single barrel module introduces high risk of circular references and forces localization modules to load unnecessary schema engines.
  When valid: Valid only in small, flat codebases where circular dependency cycles are impossible and bundling overhead is negligible.
- Inlining Error and Check Types Directly Within Each Locale (rejected)
  Rejected because: Duplicating error contracts and check structures across every localization dictionary creates divergence, maintenance drift, and type incompatibility.
  When valid: Valid only when localization dictionaries are completely decoupled external plugins with no shared runtime contracts.

## Risks

- Deep internal submodule import paths may break if internal directory structures are reorganized without migration tooling.
  Mitigation: Define and enforce explicit package export maps or internal module boundary linting rules to govern allowed import specifiers.
  Owner: Core Architecture Team
- Inadvertent introduction of backward dependencies from core submodules to localization modules.
  Mitigation: Enforce automated static dependency graph validation in continuous integration pipelines to fail builds containing cycles or forbidden import directions.
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
- When introducing a new locale bundle or adapter module, verify that imports reference only the dedicated checks, errors, and utility subpaths required for message compilation.
- Maintain strict separation between error type definitions, validation assertion checks, and general utilities to preserve modular consumption across all localization targets.

## Continuation Context


Verify commands:
- Discover and run the project repository dependency graph validation script to ensure no circular dependencies exist between core submodules and peripheral consumers.
- Discover and run the project repository static analysis and module boundary linter to verify that localization modules import only permitted core submodules.
- Discover and execute the project repository test suite to validate that all localization and compatibility modules compile and execute against core contracts.

Accept when:
- Static dependency analysis reports zero circular dependencies between internal core submodules and consumer modules.
- All localization modules successfully resolve imported checks, errors, and utilities from designated core subpaths.
- All unit and integration tests passing across all supported locales and compatibility facades.

## Enforcement

- Verified by: Automated static module boundary validation in continuous integration pipelines
- Verified by: Automated circular dependency detection scripts executed during pull request verification
- Verified by: Peer code review verification of internal import specifiers for all new localization or adapter modules
- Violation handling: Pull requests containing disallowed import paths or circular module dependencies are automatically blocked from merging.
- Violation handling: Violations identified during code review require refactoring imports to target the appropriate core submodule before approval.
- Exception process: Exceptions requiring cross-boundary imports must be submitted via architectural review with documented justification demonstrating the absence of cycles.
- Exception process: Temporary waivers must include an expiration milestone and an associated remediation issue in the project issue tracker.