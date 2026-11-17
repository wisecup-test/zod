---
version: 2
name: 64b00cb1-2ea2-48e9-b67f-615108520386-internal-core-module-integration-for-localization-modules-localization-modules-define-language-specific-grammatical
description: "Internal Core Module Integration for Localization Modules: Localization Modules Define Language Specific Grammatical"
metadata:
  actual:
    adr_id: 64b00cb1-2ea2-48e9-b67f-615108520386
    status: accepted
    candidate_group_id: a9c62ae4-f0d0-459b-84d7-cef8e7278899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/locales/**
---

# Internal Core Module Integration for Localization Modules: Localization Modules Define Language Specific Grammatical

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v4/locales/**`

## Context

- The library architecture supports multi-locale message generation across dozens of language definitions.
- Localization definitions require access to standardized validation checks, error representations, and utility routines to format error payloads accurately.
- Directly importing shared internal core modules prevents duplicated validation algorithms and ensures structural consistency across all localized error outputs.

## Problem Statement

Providing localized validation error messages across dozens of distinct locales creates a risk of diverging error structures and redundant implementations of condition checks and utility functions if individual locale modules implement logic independently.

## Decision

1. MAY: Localization modules MAY define language-specific grammatical rules and string interpolation logic while delegating validation and error structures to the core module.

## Policy Block

- MAY Localization modules MAY define language-specific grammatical rules and string interpolation logic while delegating validation and error structures to the core module.

In scope:
- All internal localization modules responsible for translating or formatting validation error messages.
- Internal core modules providing shared checks, error specifications, and utilities.

Out of scope:
- External consumer translation overrides provided at runtime outside the library codebase.
- Self-contained modules that operate independently of validation checks and error formatting.

## Rationale

- Evidence across sixty-three localization modules demonstrates a uniform reliance on internal core checks, errors, and utility modules.
- Centralizing checks and error definitions in a shared internal module guarantees that all locale definitions evaluate conditions and generate payload structures identically.
- Eliminates redundancy and reduces maintenance overhead when validation check signatures or error schemas evolve.

## Consequences

Positive:
- Uniform error reporting structures and validation check evaluation across all supported localization modules.
- Centralized maintenance of core validation logic, checks, and utilities without cascading changes across individual locale files.
- Localization modules remain lightweight translation layers focused purely on language-specific phrasing.

Negative:
- Tight dependency coupling between all localization modules and the internal core module interfaces.
- Changes to core check or error contracts necessitate auditing and updating dependent localization modules.

## Alternatives

- Self-contained localization modules containing localized validation checks and utility functions (rejected)
  Rejected because: Reimplementing checks and utilities in each locale module introduces logic drift, maintenance bloat, and inconsistent validation behavior across languages.
  When valid: Valid only in standalone single-language packages with no shared framework infrastructure.
- Dynamic runtime dependency injection of validation check and utility delegates into locale providers (rejected)
  Rejected because: Adds runtime indirection, initialization complexity, and performance overhead compared to direct internal module imports.
  When valid: Valid when locale packages are distributed as completely independent dynamic plugins loaded at runtime.

## Risks

- Breaking changes in the internal core module interface can break multiple localization modules simultaneously.
  Mitigation: Enforce strict interface contracts and comprehensive test suites across all localization modules during continuous integration.
  Owner: Core Architecture Team
- Localization contributors might attempt to bypass the core module to introduce custom validation logic.
  Mitigation: Automated linting and module boundary checks that restrict localization module imports to approved core interfaces.
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
- Verify module import paths adhere to internal architectural boundaries when authoring new locale definitions.
- Ensure error formatting templates consume parameters strictly from core error schemas to preserve contract fidelity.

## Continuation Context


Verify commands:
- Discover and run the project static analysis and linting scripts to verify module import constraints across localization modules.
- Discover and execute the repository test suite to validate locale error formatting against core check specifications.

Accept when:
- All localization modules successfully import core checks, errors, and utilities without boundary violations.
- Test suites pass for all locale modules with consistent error formatting behavior.

## Enforcement

- Verified by: Automated continuous integration checks verifying module imports and boundary compliance.
- Verified by: Peer code review for all new and modified localization modules.
- Violation handling: Pull requests with non-compliant imports or duplicated core logic are blocked from merging.
- Violation handling: Violations must be refactored to consume the shared core module before approval.
- Exception process: Exceptions require formal architectural review and approval documented in a follow-up decision record.