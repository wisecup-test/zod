# Zod Core Library Modular Architecture: Internal Core Modules Requiring Common Primitive

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Core validation and parsing libraries require foundational mechanisms for schema execution, rule checking, regex evaluation, error formation, and external standard compliance.
- Monolithic engine architectures accumulate circular dependencies and hinder targeted optimization across parsing and error-handling subsystems.
- The codebase establishes discrete internal core modules for schema definitions, validation checks, error representations, parsing pipelines, and shared utilities.
- Cross-module dependencies within the internal library layer are coordinated through explicit relative module interfaces and shared specification contracts.

## Problem Statement

Complex data validation frameworks risk tight architectural coupling and maintainability degradation when schema definitions, parsing execution pipelines, validation checks, and error handling are consolidated into monolithic structures. Without clear internal module boundaries, isolating foundational execution paths from high-level abstractions becomes difficult, increasing regression risks and preventing independent optimization of internal subsystems.

## Decision

1. MUST: Internal core modules requiring common primitive functions or string manipulations MUST route shared logic through dedicated utility modules rather than cross-importing unrelated domain modules.

## Policy Block

- MUST Internal core modules requiring common primitive functions or string manipulations MUST route shared logic through dedicated utility modules rather than cross-importing unrelated domain modules.

In scope:
- Internal core subsystems of the library responsible for parsing, schema representation, validation assertions, and error formatting
- Module boundaries linking foundational utilities to specification adapters and runtime execution pipelines

Out of scope:
- External consumer-facing schema definitions and end-user application validation layers
- Third-party consumer configuration and framework integration plugins

## Rationale

- Separating core responsibilities into dedicated internal modules establishes clear architectural boundaries, preventing tight coupling between parsing logic, check executions, and error reporting.
- Dedicated utility and specification boundary modules enable modular reuse without introducing circular dependency cycles across the core subsystem.
- Isolating standard schema adapters and error representations allows independent evolution and compliance testing without destabilizing core execution routines.

## Consequences

Positive:
- Improves code maintainability and test isolation across distinct parsing, checking, and error generation routines.
- Facilitates clear dependency graphs within the internal library architecture, reducing regression risks during optimization.
- Enables pluggable integration with external schema interoperability standards without polluting internal engine structures.

Negative:
- Increases navigation overhead and structural complexity across numerous discrete module files.
- Requires strict governance over cross-module imports to prevent accidental circular reference introduction.

## Alternatives

- Monolithic Core Module Architecture (rejected)
  Rejected because: Consolidating parsing, checks, schemas, and errors into a monolithic module creates tight coupling, increases bundle overhead, and causes circular dependency hazards during maintenance.
  When valid: Valid only in trivial single-purpose libraries where modular decomposition introduces unwarranted structural overhead.
- Independent Multi-Package Monorepo Division for Every Core Subsystem (rejected)
  Rejected because: Publishing and versioning parsing, checks, errors, and regexes as separate standalone packages introduces excessive packaging and release management friction for tightly synchronized internal mechanics.
  When valid: Valid when subsystems have independent release cycles and distinct consumer audiences across multiple unrelated ecosystems.

## Risks

- Circular dependency emergence between schema definitions, validation checks, and parsing pipelines.
  Mitigation: Enforce unidirectional dependency flows where utilities and error types remain leaf nodes relative to execution orchestrators, verified via automated structural linting.
  Owner: engineering team
- Drift between internal error representations and external standard schema specifications.
  Mitigation: Isolate external specification translation within a dedicated boundary module backed by automated contract tests.
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
- Organize internal core logic into focused, single-responsibility modules, keeping utilities and error types independent of higher-level parsing orchestration.
- Maintain unidirectional module imports across internal boundaries to ensure tree-shakability and prevent circular dependency cycles.

## Continuation Context


Verify commands:
- Discover and run the project static analysis and linting scripts to verify internal module dependency boundaries and detect circular references.
- Discover and run the project type-checking and unit test suites to validate core parsing, check execution, and error formatting integrity.

Accept when:
- All unit and contract test suites execute successfully without errors or regressions.
- Static analysis and dependency linters report zero circular dependencies across internal core modules.
- Type checking passes with zero diagnostics across all internal core module interfaces.

## Enforcement

- Verified by: Automated continuous integration checks executing dependency boundary linters and type checkers
- Verified by: Peer code review verifying adherence to modular boundaries and absence of circular imports
- Violation handling: Pull requests introducing circular dependencies or violating module segregation boundaries must be blocked and rejected until refactored.
- Exception process: Exceptions require formal architectural review and approval from the core library maintainers, accompanied by documented rationale and mitigation plans.