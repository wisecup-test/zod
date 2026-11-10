---
version: 2
name: 601a0a45-3fc8-4d9d-a638-fe80ce647d36-adoption-of-vitest-config-module-for-standardized-test-harness-configuration-test-execution-configurations-define-their-configuration
description: "Adoption of vitest/config Module for Standardized Test Harness Configuration: Test Execution Configurations Define Their Configuration"
metadata:
  actual:
    adr_id: 601a0a45-3fc8-4d9d-a638-fe80ce647d36
    status: accepted
    candidate_group_id: faecdf74-995d-4074-a45b-1d15234f9404
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - "**"
      - "!packages/bench/**"
      - "!packages/docs/**"
      - "!packages/integration/**"
      - "!packages/mini/**"
      - "!packages/resolution/**"
      - "!packages/treeshake/**"
      - "!packages/tsc/**"
      - "!packages/zod/**"
---

# Adoption of vitest/config Module for Standardized Test Harness Configuration: Test Execution Configurations Define Their Configuration

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `**` (whole repository)

Excludes:
- `packages/bench/**`
- `packages/docs/**`
- `packages/integration/**`
- `packages/mini/**`
- `packages/resolution/**`
- `packages/treeshake/**`
- `packages/tsc/**`
- `packages/zod/**`

## Context

- Test suite execution configurations exist across multiple distinct project execution contexts.
- Standardized configuration interfaces are required to maintain consistent test execution flags, runtime path resolution, and type checking across configurations.
- The codebase standardizes on the vitest/config module to provide structured configuration definition primitives.

## Problem Statement

Inconsistent test harness definitions and untyped configuration objects lead to runtime discrepancies, configuration drift, and broken path resolution across multi-target test environments.

## Decision

1. MUST: All test execution configurations MUST define their configuration objects using the defineConfig helper exported by the vitest/config module.

## Policy Block

- MUST All test execution configurations MUST define their configuration objects using the defineConfig helper exported by the vitest/config module.

In scope:
- All test harness configuration files across root and package contexts.

Out of scope:
- Application runtime configuration modules unrelated to test runners or compilation harnesses.

## Rationale

- Adopting a unified configuration builder API standardizes configuration syntax, guarantees schema enforcement, and provides type hints across compilation and execution scopes.
- Observed evidence across root and target test configuration files confirms uniform reliance on vitest/config and standard platform path utilities.

## Consequences

Positive:
- Ensures type-safe and validated configuration surfaces across all test execution layers.
- Unifies configuration factory signatures across separate execution, root, and compilation contexts.
- Eliminates divergent custom configuration wrappers across packages.

Negative:
- Tightly couples test configuration schemas to the exported types of the specific configuration library.
- Requires configuration authors to ensure resolution paths for core runtime utilities align across module systems.

## Alternatives

- Plain unvalidated object exports for test configurations (rejected)
  Rejected because: Omits schema validation, context autocompletion, and compile-time type verification.
  When valid: Minimalist environments where external configuration wrapper libraries cannot be linked.
- Bespoke internal configuration parsers (rejected)
  Rejected because: Increases maintenance burden and diverges from ecosystem test runner conventions.
  When valid: Environments with isolated custom test runners requiring unique execution contexts.

## Risks

- Upstream schema divergence or breaking changes in configuration factory options across library updates.
  Mitigation: Enforce lock-file version resolution and automate CI checks against breaking upstream configuration schema changes.
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
- Test configurations should import configuration builder primitives directly from the designated configuration module rather than composing untyped configuration hashes.
- Path resolution within configuration modules should leverage standard platform runtime modules to ensure consistent URI and path normalization across operating systems.

## Continuation Context


Verify commands:
- Discover the repository dependency manifest and lock artifact, verify the resolved dependency entry, and execute the project verification pipeline to validate configuration integrity.

Accept when:
- All test configuration definitions export structures declared through the adopted configuration factory API.
- Repository lock verification confirms synchronization between the active environment and declared dependency ranges.

## Enforcement

- Verified by: Automated static analysis verifying that test configuration files consume the designated configuration factory API.
- Verified by: Code reviews checking adherence to lock-file grounding and module isolation rules.
- Violation handling: Flagged configurations fail build and pull request checks until brought into compliance.
- Violation handling: Non-compliant configuration exports must be refactored to use the standardized configuration factory.
- Exception process: Submit an architectural exception request detailing why custom test execution flags cannot be expressed through the standard configuration factory.
- Exception process: Obtain review and sign-off from the architectural governance leads before committing unvalidated test configurations.