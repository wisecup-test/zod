---
version: 2
name: 699c8ae8-b0c4-469a-ba64-ca162eacbd49-core-library-module-architecture-runtime-method-compilation-utilize-installcompiledusermethods-wrap
description: "Core Library Module Architecture: Runtime Method Compilation Utilize Installcompiledusermethods Wrap"
metadata:
  actual:
    adr_id: 699c8ae8-b0c4-469a-ba64-ca162eacbd49
    status: accepted
    candidate_group_id: a51e0918-ebb5-4091-bf89-5c5aaedb2d07
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Core Library Module Architecture: Runtime Method Compilation Utilize Installcompiledusermethods Wrap

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v4/core/**`

## Context

- The core library engine provides foundational schema validation, compilation, and error handling capabilities across the framework.
- Performance-critical validation workflows require compilation routines to delegate parsing to specialized compiled parsers while maintaining standard public method contracts.
- Internal schema processors require dedicated caching layers and lookup registries to manage schema transformations and intermediate representation states.

## Problem Statement

Monolithic validation logic couples schema representations with compilation mechanics and runtime checks, impeding maintainability and preventing optimized execution paths from wrapping standard parsing contracts safely.

## Decision

1. MUST: Runtime method compilation MUST utilize installCompiledUserMethods to wrap core parse and safeParse entrypoints with compiled parser functions while preserving original fallback behavior.

## Policy Block

- MUST Runtime method compilation MUST utilize installCompiledUserMethods to wrap core parse and safeParse entrypoints with compiled parser functions while preserving original fallback behavior.

In scope:
- Internal core library modules responsible for schema definition, compilation routines, and validation checks.
- Runtime compilation and method installation mechanisms wrapping parser functions.

Out of scope:
- Public consumer applications invoking external high-level validation APIs.
- External utility extensions operating outside the core library module boundary.

## Rationale

- Decomposing core responsibilities into specialized modules isolates compilation optimizations from schema definition primitives.
- Wrapping standard parse and safeParse functions via installCompiledUserMethods enables performance gains from compiled parsers while preserving backward-compatible execution fallbacks.
- Contextual caching and lookup layers reduce redundant work across repeated schema transformations and compilation passes.

## Consequences

Positive:
- Isolates schema compilation and user method installation from underlying validation check logic.
- Improves parsing throughput by delegating execution to compiled functions with safe fallback mechanisms.
- Provides dedicated lookup layers and caching mechanisms for efficient schema transformation and resolution.

Negative:
- Inter-module dependencies within the core subsystem require disciplined dependency hygiene to prevent circular imports.
- Compiler state management and cache tracking introduce memory considerations during complex schema generation.

## Alternatives

- Monolithic core engine consolidating checks, parsing, and compilation into a single module (rejected)
  Rejected because: Creates excessive coupling between validation rules and compilation logic, hindering independent testing and modular extensibility.
  When valid: Small standalone validation scripts where subsystem decomposition adds unwarranted overhead.
- Uncached dynamic evaluation without compiled user method wrappers (rejected)
  Rejected because: Imposes significant runtime parsing overhead by re-evaluating schema rules on every invocation instead of delegating to optimized compiled parsers.
  When valid: One-off schema executions where compilation and cache coordination costs exceed execution time.

## Risks

- Complex dependency chains between core modules could introduce circular dependencies.
  Mitigation: Enforce strict module hierarchy rules and automated linting to prevent cyclic cross-module imports.
  Owner: Engineering Team
- In-memory compiler lookup caches could retain obsolete references in long-running evaluation loops.
  Mitigation: Explicitly clear contextual constants and registries upon completion of schema processing runs.
  Owner: Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- When installing compiled methods via installCompiledUserMethods, wrap target parse and safeParse functions with fallback delegation to original source implementations.
- Scope contextual compiler caches and state mappings to active evaluation cycles to prevent unbounded memory growth.

## Continuation Context


Verify commands:
- Discover and execute the repository build verification script to validate module resolution across all core library boundaries.
- Discover and run the project test suite targeting core schema compilation, parsing, and validation check routines.
- Discover and run the repository static type checker and module linting tools to confirm interface compliance and absence of circular references.

Accept when:
- All unit tests covering core schema compilation, parsing, and check validations pass cleanly.
- Static type analysis confirms that function signatures and compiled method wrappers adhere to declared interfaces with zero type errors.
- Module boundary analysis verifies no undeclared cyclic references exist between core library modules.

## Enforcement

- Verified by: Continuous integration suites verifying module boundaries and running core unit tests.
- Verified by: Static type checking ensuring structural compliance with compiled function and schema interfaces.
- Verified by: Code reviews by core library maintainers for any changes to internal module structure.
- Violation handling: Automated build failures on circular dependencies or unauthorized module boundary violations.
- Violation handling: Rejection of pull requests that mutate public parser contracts without using approved installation wrappers.
- Exception process: Engineers must submit an architectural exception request detailing technical blockers to core module decoupling.
- Exception process: Exceptions require unanimous approval from core library maintainers and must include an issue tracker reference for future remediation.