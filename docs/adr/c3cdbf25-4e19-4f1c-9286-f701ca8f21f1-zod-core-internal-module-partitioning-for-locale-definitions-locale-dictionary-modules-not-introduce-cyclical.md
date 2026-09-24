# Zod Core Internal Module Partitioning for Locale Definitions: Locale Dictionary Modules Not Introduce Cyclical

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- The validation library provides multi-language error messaging across numerous global locales.
- Localization dictionaries format error messages and validate check parameters without importing the complete validation runtime.
- Decoupled internal core submodules provide atomic check definitions, error structures, and string formatting utilities.

## Problem Statement

Coupling localization message dictionaries directly to monolithic library exports or schema definition engines introduces circular dependencies and forces client applications to bundle unused runtime parsers when loading specific language dictionaries.

## Decision

1. MUST_NOT: Locale dictionary modules MUST NOT introduce cyclical dependencies by importing parser engines, composite schema builders, or top-level validator singletons.

## Policy Block

- MUST_NOT Locale dictionary modules MUST NOT introduce cyclical dependencies by importing parser engines, composite schema builders, or top-level validator singletons.

In scope:
- Implementation and maintenance of language locale modules within the validation library package.
- Internal core module interface consumption for error issue reporting and message localization.

Out of scope:
- External consumer applications that define custom error maps through the public client API.
- Schema parser execution logic and core type validation routines.

## Rationale

- Restricting locale modules to internal core submodules guarantees decoupling between language-specific message catalogs and schema validation engines, eliminating circular reference risks.
- Direct dependency on granular core submodules minimizes consumer bundle sizes by ensuring that importing a single locale dictionary does not transitively bundle the full schema parsing suite.
- Centralizing error types and check definitions within internal core submodules ensures that every localization module conforms to identical issue contracts and diagnostic structures.

## Consequences

Positive:
- Eliminates circular dependencies between validation schemas, runtime parsers, and localization error maps.
- Enables fine-grained tree-shaking so applications only ship the specific locale dictionaries they require.
- Enforces consistent diagnostic issue contracts across all localized language packs.

Negative:
- Requires maintaining strict architectural boundaries between internal core submodules and presentation modules.
- Internal changes to core error descriptors or utility contracts require coordinated updates across all locale files.

## Alternatives

- Importing types and utilities directly from the monolithic package entrypoint (rejected)
  Rejected because: Introduces circular dependencies between the main package exports and locale bundles, substantially increasing bundle size for consumers importing single language packs
  When valid: Small monolithic packages where tree-shaking and standalone localized error maps are not required
- Embedding localization strings directly inside individual schema definition modules (rejected)
  Rejected because: Couples schema parsing logic to specific human languages and prevents decoupled internationalization and independent dictionary contribution
  When valid: Single-language applications with no requirement for multi-language error messaging

## Risks

- Breaking interface changes in internal core submodules may cause drift or compilation failures across individual locale dictionaries.
  Mitigation: Establish automated continuous integration test suites that compile and validate all locale dictionaries against the core interfaces.
  Owner: engineering team
- Contributors might accidentally import higher-level schema modules into new locale definitions.
  Mitigation: Enforce module boundary lint rules and import boundary static analysis checks in the continuous integration pipeline.
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
- When creating a new locale module, import only the check descriptors, error types, and formatting utility helpers from the internal core submodules.
- Ensure all error messages parameterized with input values or type expectations use the standardized utility formatting functions rather than custom string concatenation.

## Continuation Context


Verify commands:
- Discover the project test runner from repository configuration and execute the localization test suite.
- Discover the project module boundary linter and execute static dependency analysis to verify no circular or monolithic imports exist.
- Discover the build script from the package configuration and execute a production compile to verify bundle decoupling.

Accept when:
- All locale definitions compile cleanly and pass their respective message formatting test cases.
- Dependency linting confirms that localization modules import only designated internal core submodules without circular dependencies.
- Module bundle inspection verifies that importing an individual locale dictionary does not pull in unreferenced schema parsers.

## Enforcement

- Verified by: Automated static analysis and module boundary lint rules executed during continuous integration.
- Verified by: Pull request code reviews by package maintainers verifying import paths for new and modified locale modules.
- Violation handling: Pull requests introducing unauthorized imports from top-level schema modules or cyclic dependencies will fail automated checks and be blocked from merging.
- Exception process: Proposals to introduce new core submodule dependencies must be submitted via an architectural RFC and approved by the core library maintainers.