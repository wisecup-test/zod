---
version: 2
name: 7f7d6cf2-75b5-4a4b-9d12-8a6ac8220f8c-internal-core-module-architecture-for-schema-engine-and-processing-subsystems-compiled-schema-evaluation-pathways-install-execution
description: "Internal Core Module Architecture for Schema Engine and Processing Subsystems: Compiled Schema Evaluation Pathways Install Execution"
metadata:
  actual:
    adr_id: 7f7d6cf2-75b5-4a4b-9d12-8a6ac8220f8c
    status: accepted
    candidate_group_id: 6af386df-1645-4617-9e12-ca356ef23697
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/**
---

# Internal Core Module Architecture for Schema Engine and Processing Subsystems: Compiled Schema Evaluation Pathways Install Execution

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v4/**`

## Context

- Schema engine subsystems require a distinct separation between foundational type definitions, runtime validation execution, format conversion, and code generation.
- Multiple core processing modules rely on shared registries, error structures, and validation utilities across distinct execution phases.
- Decoupling core schema mechanics from translation and compilation targets allows independent optimization and tree-shaking across library modules.

## Problem Statement

Without an explicit modular architecture separating core schema definitions and registries from specialized compilation and format conversion layers, shared validation logic becomes duplicated, tightly coupled to specific formats, and difficult to optimize or maintain.

## Decision

1. SHOULD: Compiled schema evaluation pathways SHOULD install compiled execution methods over runtime parsers while preserving fallback behavior when invalid markers are encountered.

## Policy Block

- SHOULD Compiled schema evaluation pathways SHOULD install compiled execution methods over runtime parsers while preserving fallback behavior when invalid markers are encountered.

In scope:
- Internal library modules implementing core schema primitives, registries, error handlers, and utility routines.
- Compiler and format conversion subsystems interacting with foundational schema models.

Out of scope:
- End-user application code consuming the public facade of the library.
- Standalone third-party utility scripts operating outside the library core architecture.

## Rationale

- Evidence across the internal library modules indicates consistent reliance on shared core modules for checks, error handling, registries, and utilities, establishing an intentional core modular tier.
- Isolating core schemas and registries from compiler optimizations and format translators prevents circular dependencies and protects core execution performance.
- Managing references and cache structures within scoped context objects ensures safe concurrent validation and deterministic compilation.

## Consequences

Positive:
- Clear separation of concerns between core validation mechanics, compilation passes, and format converters.
- Enables targeted performance optimizations in compilation and registry lookups without impacting baseline schema behavior.
- Improves modularity and maintainability across internal library subsystems.

Negative:
- Requires disciplined maintenance of module boundaries and import hierarchies to prevent circular references.
- Context tracking and registry abstractions introduce architectural indirection compared to inline procedural logic.

## Alternatives

- Monolithic Single-Module Architecture (rejected)
  Rejected because: Combining schema definitions, compiler logic, error formatting, and format converters into a single module degrades maintainability, creates tight coupling, and prevents modular consumption.
  When valid: Appropriate only for minimal, single-purpose micro-libraries without multi-target compilation or serialization adapters.
- Dynamic Plugin Architecture with Runtime Service Registration (deferred)
  Rejected because: Dynamic runtime registration of core validation primitives introduces lookup overhead and reduces static analysis guarantees compared to internal modular imports.
  When valid: Useful when third-party extensions must register novel schema primitives dynamically at runtime without recompilation.

## Risks

- Tight coupling between internal core modules can lead to circular dependencies if boundaries are relaxed.
  Mitigation: Enforce strict one-way dependency rules and automated architectural boundary linting.
  Owner: Engineering team
- Overhead in maintaining synchronized registry state and contextual reference maps across compilation and execution passes.
  Mitigation: Encapsulate registry operations behind explicit context accessors with scoped lifecycle cleanup.
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
- Ensure core module exports expose stable interfaces for schemas, registries, and error constructs that external modules can depend upon reliably.
- Maintain isolated registry and traversal context lifecycles during compilation and conversion routines to avoid memory leaks or state contamination.

## Continuation Context


Verify commands:
- Run the project test suite to verify internal core module boundaries and schema compilation passes all functional suites.
- Execute the repository linting and module boundary checks to ensure no circular imports or disallowed core module references exist.
- Execute the project typechecker to confirm strict type safety across core schema exports and registry interfaces.

Accept when:
- All internal module boundary tests and schema validation suites pass without errors.
- Dependency and type validation checks complete with zero circular reference or boundary violations.
- Runtime compilation methods match baseline parser behavior for all defined schema inputs.

## Enforcement

- Verified by: Static module boundary analysis in the continuous integration pipeline.
- Verified by: Peer review focusing on dependency direction between core modules and peripheral adapters.
- Verified by: Automated unit and integration test coverage across schema processing layers.
- Violation handling: Pull requests introducing circular dependencies between core modules and external adapters will be rejected.
- Violation handling: Non-compliant direct access to internal schema structures bypassing registry accessors must be refactored prior to merge.
- Exception process: Exceptions require architectural review and explicit sign-off by library maintainers with documented justification and remediation plans.