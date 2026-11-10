---
version: 2
name: 8cecb3c4-4576-4d82-baad-599c8488767f-internal-core-module-for-shared-validation-primitives-interactions-between-peripheral-feature-modules-internal
description: "Internal Core Module for Shared Validation Primitives: Interactions Between Peripheral Feature Modules Internal"
metadata:
  actual:
    adr_id: 8cecb3c4-4576-4d82-baad-599c8488767f
    status: accepted
    candidate_group_id: 6f1a4916-3848-4f86-b843-16c190a6b899
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module for Shared Validation Primitives: Interactions Between Peripheral Feature Modules Internal

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v4/**`

## Context

- The codebase contains numerous localized dictionary files and compatibility layers that require access to common validation checks, error structures, and utility routines.
- Duplicating core error formats and check primitives across independent localized files introduces divergence risks and increases maintenance overhead.
- Centralizing shared operational utilities into a dedicated core module establishes a single source of truth for runtime validation primitives.

## Problem Statement

Maintaining sixty-six peripheral modules, including extensive locale dictionaries and compatibility adapters, without a centralized internal core module leads to code duplication, divergent error formats, and inconsistent check semantics across validation targets.

## Decision

1. SHOULD: Interactions between peripheral feature modules and internal core submodules SHOULD be restricted to exposed interfaces for checks, errors, utilities, and visitor traversals.

## Policy Block

- SHOULD Interactions between peripheral feature modules and internal core submodules SHOULD be restricted to exposed interfaces for checks, errors, utilities, and visitor traversals.

In scope:
- Implementation of localization dictionaries and error message mappings
- Implementation of schema adapters and compatibility translation layers
- Creation of peripheral extensions requiring shared validation checks or error structures

Out of scope:
- Independent standalone packages that do not share the internal core runtime
- Self-contained utility modules with zero validation or schema dependencies

## Rationale

- Uniform adoption of core checks and error structures across sixty-six modules guarantees structural consistency in validation output.
- Centralizing visitor traversals and utilities within the core module minimizes bundle duplication and simplifies maintenance.
- Decoupling localized dictionaries from execution logic while linking them through standardized core interfaces preserves extensibility.

## Consequences

Positive:
- Standardized error handling and check semantics across all locale definitions and schema layers.
- Reduced duplication of common inspection, traversal, and utility routines across peripheral modules.
- Clear dependency hierarchy directing peripheral feature modules inward toward foundational core primitives.

Negative:
- Tight coupling of peripheral feature modules to internal core module contracts.
- Refactoring core module interfaces requires coordinated updates across all dependent locale and compatibility modules.

## Alternatives

- Independent Error and Check Definitions per Locale Module (rejected)
  Rejected because: Duplicating check functions and error schemas across dozens of locale files leads to semantic drift and high maintenance overhead.
  When valid: Only viable when target locales require fundamentally incompatible validation architectures.
- Monolithic Single-File Module Architecture (rejected)
  Rejected because: Inlining all checks, utilities, and localization tables into a single module degrades tree-shaking efficiency and code readability.
  When valid: Acceptable only in minimal single-file micro-libraries with no internationalization requirements.

## Risks

- Breaking changes in core module exports can propagate failures across all consuming localization modules.
  Mitigation: Enforce contract stability through strict interface testing and comprehensive automated regression suites.
  Owner: Core engineering team
- Circular dependencies introduced if core utilities inadvertently import peripheral modules.
  Mitigation: Automate architectural boundary linting to reject any outward dependencies from core modules.
  Owner: Architecture review team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Ensure newly authored localization dictionaries import error definitions and validation checks exclusively from the core module namespace.
- Verify that all imported core utility methods and visitor contracts preserve backward compatibility when extending schema traversal logic.

## Continuation Context


Verify commands:
- Discover the project verification script from the repository manifest and execute static analysis to validate module import paths.
- Discover and run the project test suite to verify that all localization and compatibility modules satisfy core module interface contracts.

Accept when:
- Static analysis confirms zero circular dependencies and verifies all peripheral modules import shared primitives from the internal core module.
- All automated test suites pass without interface contract mismatches or unhandled validation errors.

## Enforcement

- Verified by: Automated continuous integration checks validating static import boundaries.
- Verified by: Peer code review for all pull requests modifying core interfaces or adding localization files.
- Violation handling: Continuous integration builds fail upon detection of unauthorized dependency paths or duplicate validation primitives.
- Violation handling: Pull requests violating inward module boundaries are blocked until refactored.
- Exception process: Submit an architectural review request detailing technical constraints preventing reliance on the core module.
- Exception process: Temporary exceptions require formal sign-off from the core architecture team with a scheduled remediation plan.