# Zod Core Library Module Decomposition: Subsystem Isolation of Schemas, Parsing, and Validation Registries: Input Parsing Pipelines Coordinate Passes Through

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Core schema validation engines require high extensibility, predictable execution paths, and clean isolation between data contracts and runtime evaluation.
- Monolithic engine architectures couple schema structural declarations with parsing mechanics, error aggregation, and global registries, increasing maintenance overhead and circular dependency risks.
- The codebase exhibits a decomposed module topology where schema definitions, validation checks, error definitions, parsing engines, and registries reside in dedicated internal sub-modules connected by discrete interface boundaries.
- Compatibility layers adapt these decoupled core subsystems to maintain external backward compatibility while preserving core architectural isolation.

## Problem Statement

Validation libraries frequently suffer from tight coupling when schema declarations, parsing execution logic, error structures, and validation rules are conflated into monolithic source units. This coupling creates circular module dependencies, complicates targeted optimization of the parsing pipeline, and obstructs the evolution of external APIs without breaking internal execution mechanisms.

## Decision

1. MUST: Input parsing pipelines MUST coordinate parsing passes through dedicated parse utilities while remaining decoupled from concrete schema construction APIs.

## Policy Block

- MUST Input parsing pipelines MUST coordinate parsing passes through dedicated parse utilities while remaining decoupled from concrete schema construction APIs.

In scope:
- Implementation and extension of internal schema definitions, parse runners, validation checks, and error formatting modules.
- Architecture boundary definitions between public library APIs, compatibility wrappers, and internal core subsystems.

Out of scope:
- Consumer-facing application code utilizing the published validation library API.
- External third-party integration plugins that do not modify internal core engine subsystems.

## Rationale

- Evidence across multiple core module files demonstrates consistent separation of concerns, where checks, errors, parsing, and schemas are partitioned into independent modules.
- Decomposing the core validation engine prevents circular dependencies during module loading and ensures that execution pathways can be compiled and analyzed independently.
- Encapsulating registry access and cache resolution behind dedicated interfaces provides predictable metadata lookup and state isolation across validation runs.
- Isolating the internal core allows compatibility facades to bridge different major API generations without polluting core parsing primitives.

## Consequences

Positive:
- Subsystem isolation minimizes blast radius when modifying validation check logic, error structures, or parsing mechanics.
- Elimination of circular dependencies enhances static analysis precision, dead code elimination, and bundling efficiency.
- Modular boundaries facilitate targeted unit testing of parser routines and schema definitions in isolation.

Negative:
- Module decomposition increases the number of internal interface boundaries and relative import linkages across the codebase.
- Cross-cutting features touching schema definitions, checks, and parsing require coordinated changes across multiple internal modules.

## Alternatives

- Monolithic Core Architecture Combining Schemas, Parsing, and Checks in Single Module (rejected)
  Rejected because: A monolithic architecture creates circular reference chains, impedes dead code elimination, and prevents modular extension of parse and check subsystems.
  When valid: Valid only in small proof-of-concept libraries with minimal schema varieties and trivial parsing logic.
- Complete Micro-Package Monorepo Decomposition for Every Core Subsystem (rejected)
  Rejected because: Publishing each internal core subsystem as an independent external package introduces substantial version management overhead and packaging friction without proportional operational benefit.
  When valid: Valid when core subsystems must be distributed independently across entirely distinct runtime ecosystems.

## Risks

- Circular dependency introduction when adding complex cross-subsystem features between schemas and parse utilities
  Mitigation: Enforce automated module boundary checks during continuous integration to fail builds that introduce circular import paths
  Owner: engineering team
- Interface drift between compatibility adapters and core execution primitives
  Mitigation: Validate compatibility test suites against core internal contracts across test validation runs
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
- Maintain strict internal layering where foundational utilities and error definitions do not import higher-level schema constructs or parsing orchestrators.
- Expose public capabilities through designated API facade entry points rather than allowing consumers to import internal subsystem files directly.

## Continuation Context


Verify commands:
- Discover the workspace task runner configuration and execute the project validation script to ensure module boundary constraints are satisfied.
- Inspect the root configuration to identify the static type checking task and execute it across all internal core modules.
- Execute the discovered test execution script targeting internal module unit suites to verify parse and check subsystem behavior.

Accept when:
- All internal module imports resolve cleanly across core subsystem boundaries without circular dependency warnings.
- Static type analysis and architectural boundary checks pass across all library modules with zero diagnostic errors.
- The discovered test suite completes with all assertions passing for schema evaluation, parsing, and error reporting.

## Enforcement

- Verified by: Static analysis and architectural boundary linters executed in continuous integration pipelines.
- Verified by: Mandatory architectural peer review on changes affecting core module exports and internal boundary contracts.
- Violation handling: Pull requests violating internal module isolation or introducing circular dependencies are blocked from merging.
- Violation handling: Detected boundary violations must be refactored into designated subsystem modules prior to integration.
- Exception process: Temporary architectural exceptions require documented justification and sign-off from the library architectural deciders.