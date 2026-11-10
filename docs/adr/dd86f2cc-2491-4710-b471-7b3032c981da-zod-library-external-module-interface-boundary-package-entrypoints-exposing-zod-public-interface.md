---
version: 2
name: dd86f2cc-2491-4710-b471-7b3032c981da-zod-library-external-module-interface-boundary-package-entrypoints-exposing-zod-public-interface
description: "Zod Library External Module Interface Boundary: Package Entrypoints Exposing Zod Public Interface"
metadata:
  actual:
    adr_id: dd86f2cc-2491-4710-b471-7b3032c981da
    status: accepted
    candidate_group_id: f81b1c2a-31a4-4cd6-90ee-06cb363b9402
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/**
      - src/v4/**
---

# Zod Library External Module Interface Boundary: Package Entrypoints Exposing Zod Public Interface

Status: proposed
Date: 2025-05-15
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v3/**`
- `src/v4/**`

## Context

- Multiple package distribution targets require uniform exposure of public API interfaces while isolating internal schema machinery.
- Direct export of internal core implementations across entrypoints causes tight coupling between distribution artifacts and internal compiler structures.
- Centralizing public API re-exports through an external boundary module establishes a single point of enforcement for public contract stability.

## Problem Statement

Exposing internal library implementation details directly across diverse distribution entrypoints creates tight coupling, increases the risk of leaking unstable internal abstractions, and complicates cross-variant compatibility maintenance for the Zod schema library.

## Decision

1. MUST: Package entrypoints exposing the Zod public interface MUST route all external surface exports through a dedicated external boundary module rather than exposing internal core implementations directly.

## Policy Block

- MUST Package entrypoints exposing the Zod public interface MUST route all external surface exports through a dedicated external boundary module rather than exposing internal core implementations directly.

In scope:
- Applies to all public distribution entrypoints and package export targets for the Zod library.
- Applies when defining or refactoring public module interface boundaries across library variants.

Out of scope:
- Does not apply to internal test suites, benchmarking modules, or private build helper scripts.
- Does not apply to isolated internal core submodules that do not expose public contracts.

## Rationale

- Standardizing on a dedicated external interface boundary decouples public API exposure from internal schema representations across all distribution entrypoints.
- Evidence across multiple library entrypoints confirms that routing public exports through an external boundary module maintains contract uniformity across distribution variants.
- Enforcing a boundary module prevents accidental exposure of internal helper structures and simplifies auditing of public API surface changes.

## Consequences

Positive:
- Provides clean architectural separation between internal core engine logic and consumer-facing library exports.
- Enables independent evolution of internal schema representations without mutating public consumer interfaces.
- Ensures consistency across parallel distribution targets by channeling external contracts through an authoritative boundary.

Negative:
- Introduces an intermediate indirection layer that requires maintainers to update export bindings when expanding the public interface.
- Requires strict review discipline to ensure internal submodules are not inadvertently imported directly by consumers.

## Alternatives

- Direct export of internal core schema modules from package entrypoints (rejected)
  Rejected because: Exposes internal representation details directly to consumers and creates fragile couplings that hinder internal refactoring.
  When valid: Only viable in single-file or minimal prototype libraries without multiple distribution targets.
- Independent public interface definitions per distribution variant without a shared boundary module (rejected)
  Rejected because: Leads to drift between distribution targets and duplicate export maintenance across variant entrypoints.
  When valid: Acceptable when distribution variants have entirely disjoint public contracts with no shared surface.

## Risks

- Indirection overhead could lead developers to bypass the external boundary module during rapid feature development.
  Mitigation: Automate module boundary verification in continuous integration pipelines to reject direct internal module imports.
  Owner: Engineering team
- Unsynchronized external boundary exports between distinct variant entrypoints could create unexpected interface discrepancies.
  Mitigation: Perform automated export signature comparison across entrypoints to verify consistency before publishing releases.
  Owner: Engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Maintainers must channel new public API capabilities through the designated external interface boundary module rather than directly exposing internal implementation structures.
- Verify that all distribution entrypoints import and re-export the unified external module to avoid accidental divergence in public contract definitions.

## Continuation Context


Verify commands:
- Discover and run the repository interface validation and type check scripts to verify module boundary conformance.
- Discover and run the project test suite to verify that all distribution entrypoint exports satisfy expected public contract behaviors.

Accept when:
- All distribution entrypoint exports pass repository interface and type validation checks without boundary violations.
- All public interface contract test suites pass successfully across all distribution variants.

## Enforcement

- Verified by: Continuous integration type checking and boundary linting scripts discovered from repository configurations.
- Verified by: Peer code review auditing all modifications to package entrypoints and external interface boundary modules.
- Violation handling: Pull requests introducing direct imports of internal modules from entrypoints or bypassing external boundary modules are blocked from merging until corrected.
- Exception process: Exceptions require documented architectural justification and formal sign-off from module maintainers.