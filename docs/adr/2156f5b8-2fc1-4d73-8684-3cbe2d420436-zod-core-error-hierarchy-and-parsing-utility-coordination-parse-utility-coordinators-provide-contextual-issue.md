# Zod Core Error Hierarchy and Parsing Utility Coordination: Parse Utility Coordinators Provide Contextual Issue

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- The validation engine requires structured separation between schema parse execution, error message localization, and internal parsing utilities.
- Parsing workflows emit validation issues that depend on standardized error structures defined in a centralized error module.
- Localized error mapping functions format validation failure descriptions by referencing standardized issue codes and shared utility logic.
- Parse utility routines coordinate validation issue collection without inlining locale-specific formatting strings directly into evaluation paths.

## Problem Statement

Directly embedding locale-specific error strings into parsing operations couples validation logic to presentation concerns, complicating multi-language support and preventing unified error aggregation. A structured architectural boundary is required to separate parse execution utilities from localized error maps while binding both to a common error class hierarchy.

## Decision

1. MAY: Parse utility coordinators MAY provide contextual issue metadata overrides when invoking error map formatters during recursive schema traversal.

## Policy Block

- MAY Parse utility coordinators MAY provide contextual issue metadata overrides when invoking error map formatters during recursive schema traversal.

In scope:
- Validation schema parse execution utilities
- Localized validation error formatting maps
- Internal error class definitions and issue constructors

Out of scope:
- External consumer application display formatting layers
- Third-party transport protocol serialization adapters

Exceptions:
- EX-20-001: Custom standalone schema types supply an explicit inline error message override during schema construction

## Rationale

- Centralizing error types in a dedicated error hierarchy ensures consistent issue structures across all schema validation routines.
- Isolating localization formatters from core parsing utilities enables independent extension of localized messages without modifying core evaluation pipelines.
- Consolidating common type inspections into shared utility modules prevents divergence in type-to-string representations across distinct parse helpers.

## Consequences

Positive:
- Validation logic remains decoupled from language-specific error messages.
- Unified error hierarchy guarantees predictable issue data structures for downstream consumers.
- Shared helper utilities ensure consistent type inspection across parsing and error reporting components.

Negative:
- Indirection between parse utilities and error maps introduces an additional lookup step during failure paths.
- Adding new validation issue codes requires synchronized updates across error definitions, locale tables, and parsing utilities.

## Alternatives

- Inlining localized error strings directly within parse utility evaluation routines (rejected)
  Rejected because: Couples core validation execution to specific natural language strings and prevents modular localization
  When valid: Single-locale micro-utilities where binary bundle size supersedes modularity requirements
- Delegating all error string synthesis entirely to downstream consumer applications without providing base locale maps (rejected)
  Rejected because: Forces every consumer to author comprehensive issue formatters before receiving intelligible validation failures
  When valid: Headless protocol validation engines where human-readable error strings are explicitly out of specification

## Risks

- Desynchronization between new validation issue codes in core parsing routines and localized error map handlers
  Mitigation: Enforce exhaustive type checking over issue code union types during automated test verification
  Owner: Validation Framework Maintainers
- Performance overhead from indirect error map invocations on deeply nested schema validation failures
  Mitigation: Defer error map evaluation until parsing yields failure states rather than pre-allocating error contexts on success paths
  Owner: Validation Framework Maintainers

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Implementers must discover the project repository layout to locate parsing utility modules and locale definitions before introducing new error types.
- Error maps should accept standardized issue context objects and return structured message strings conforming to the central error definition.

## Continuation Context


Verify commands:
- Discover the project verification script from the repository manifest and execute the test suite governing validation parsing and error mapping.
- Execute the repository type verification script to ensure all issue codes handled in error maps match the central error definitions exhaustively.

Accept when:
- The discovered test suite completes with all parsing utility and error map assertions passing without errors.
- Static type analysis confirms zero missing issue code branches across all registered locale formatters.

## Enforcement

- Verified by: Automated continuous integration test and type verification pipelines
- Verified by: Peer code review for pull requests modifying parsing utilities or error maps
- Violation handling: Pull requests introducing hardcoded localized messages in parsing routines or missing issue mappings will be rejected.
- Violation handling: Type check failures in continuous integration block merge until complete issue parity is restored.
- Exception process: Submit an architectural review request detailing the constraints that necessitate deviating from the central error mapping architecture.
- Exception process: Obtain explicit sign-off from the framework maintenance team before merging custom error handling paths.