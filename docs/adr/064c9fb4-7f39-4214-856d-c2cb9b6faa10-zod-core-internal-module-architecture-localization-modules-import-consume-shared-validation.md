---
version: 2
name: 064c9fb4-7f39-4214-856d-c2cb9b6faa10-zod-core-internal-module-architecture-localization-modules-import-consume-shared-validation
description: "Zod Core Internal Module Architecture: Localization Modules Import Consume Shared Validation"
metadata:
  actual:
    adr_id: 064c9fb4-7f39-4214-856d-c2cb9b6faa10
    status: accepted
    candidate_group_id: a22d8aec-faab-4dfb-9104-b031f65251b9
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Zod Core Internal Module Architecture: Localization Modules Import Consume Shared Validation

Status: proposed
Date: 2025-02-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v4/**`

## Context

- The validation library requires comprehensive internationalization support across dozens of languages without diverging from core error formatting standards.
- Maintaining independent error handling logic or validation check evaluations across dozens of localization targets introduces high maintenance overhead and behavioral inconsistencies.
- The codebase establishes an internal core module subsystem that encapsulates foundational error constructs, check definitions, and shared string manipulation utilities.
- Decoupling locale message mappings while binding them directly to shared internal core primitives ensures architectural coherence across the entire localization catalog.

## Problem Statement

Managing localized validation error messages across numerous languages risks fragmentation, code duplication, and inconsistent error payloads if individual locales implement bespoke checking or error structuring logic. A standardized architectural convention is required to decouple language-specific phrasing while enforcing unified consumption of core check types, error schemas, and utility routines.

## Decision

1. MUST: Localization modules MUST import and consume shared validation checks, error representations, and utility helpers exclusively from the internal core library modules.

## Policy Block

- MUST Localization modules MUST import and consume shared validation checks, error representations, and utility helpers exclusively from the internal core library modules.

In scope:
- All localization definitions and internationalization message formatting modules within the library.
- Extensions and contributions providing new language message maps.

Out of scope:
- Core engine validation logic and primary schema parsers.
- Independent consumer applications consuming the compiled public library interface.

## Rationale

- Static analysis reveals that sixty-two locale definitions uniformly import shared core modules rather than re-implementing error handling or type checking.
- Centralizing validation checks and error schema definitions inside internal core modules guarantees that any structural schema updates automatically propagate across all locale implementations.
- Restricting locale modules to message resolution against internal core utilities minimizes the footprint of language-specific files and simplifies contribution workflows.

## Consequences

Positive:
- Consistent error structure and issue code handling across all supported language targets.
- Elimination of duplicated check logic and redundant string manipulation routines across localization files.
- Reduced cognitive overhead for internationalization contributors who only need to map localized strings to standardized core error definitions.

Negative:
- Changes to internal core error signatures require simultaneous updates or backwards compatibility across all sixty-two locale definitions.
- Localizations are tightly bound to the internal core module export contract and cannot easily deviate for unique language-specific error architectures without core changes.

## Alternatives

- Autonomous Self-Contained Locale Modules (rejected)
  Rejected because: Requiring each locale definition to implement its own error checking and formatting utilities causes severe code duplication across dozens of files and risks divergent error shapes.
  When valid: Valid when internationalization requirements demand completely isolated, independently packaged micro-modules with zero shared dependencies.
- Global Monolithic Localization Dictionary (rejected)
  Rejected because: Consolidating all language translations into a single dictionary module inflates bundle size for consumers who only require a single target locale and tightly couples unrelated language translations.
  When valid: Valid in simple applications supporting a fixed, small set of languages where granular bundle splitting is unnecessary.

## Risks

- Breaking changes in the internal core error contracts may invalidate existing localized message mappings across multiple languages simultaneously.
  Mitigation: Enforce contract stability through automated regression test suites that validate every locale module against the core schema specification during continuous integration.
  Owner: Core library engineering team
- Contributors of new locales may inadvertently introduce ad-hoc utility logic instead of leveraging internal core functions.
  Mitigation: Incorporate static analysis rules and review checklists verifying that localization files only import permitted internal core utilities.
  Owner: Core library engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Discover the internal core module export surface to identify available check types, error models, and string utility routines before authoring new locale definitions.
- Ensure all localized message factories conform to the error formatting signature expected by the core error handling subsystem.

## Continuation Context


Verify commands:
- Discover the project task runner configuration and execute the static type-checking and linting suites to ensure locale imports satisfy internal core module boundaries.
- Discover the test suite execution script from the repository manifest and run all localization unit tests to verify error formatting consistency against core expectations.

Accept when:
- All localization modules resolve imports directly against the internal core module boundary without missing exports or type errors.
- Automated localization test suites execute and pass across all registered locale targets.
- No duplicate validation check definitions or uncoordinated error structures exist across localization files.

## Enforcement

- Verified by: Automated static analysis and type checks verifying import boundaries on every pull request.
- Verified by: Unit test suites executing message formatting validations across all locale modules.
- Verified by: Peer review by library maintainers for any newly proposed localization modules.
- Violation handling: Pull requests introducing foreign imports or duplicated check logic into localization modules will fail automated checks and require remediation before merge.
- Violation handling: Discovered regressions or non-conforming locale definitions will be tracked as blocking issues.
- Exception process: Exceptions requiring custom formatting logic must be submitted as architectural change requests to core maintainers, seeking extension of internal core utilities rather than localized workarounds.