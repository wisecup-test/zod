---
version: 2
name: 06516c3a-7668-4b7d-93dd-bb6446212980-vitest-configuration-composition-for-unit-testing-global-test-environment-lifecycle-assertions-fixtures
description: "Vitest Configuration Composition for Unit Testing: Global Test Environment Lifecycle Assertions Fixtures"
metadata:
  actual:
    adr_id: 06516c3a-7668-4b7d-93dd-bb6446212980
    status: accepted
    candidate_group_id: baa2b941-9eff-40d1-af1e-1b8fcd3b43b1
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/docs/**
      - packages/resolution/**
      - packages/zod/**
      - scripts/**
      - vitest.config.ts
---

# Vitest Configuration Composition for Unit Testing: Global Test Environment Lifecycle Assertions Fixtures

Status: proposed
Date: 2025-05-15
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `packages/docs/**`
- `packages/resolution/**`
- `packages/zod/**`
- `scripts/**`
- `vitest.config.ts`

## Context

- The repository maintains multiple packages requiring consistent unit test execution parameters and quality gates.
- Duplicating test runner options across every package leads to configuration drift and maintenance overhead.
- Unit test execution requires centralized test lifecycle hooks for global behavior enforcement such as console error traps.

## Problem Statement

Managing disparate test runner configurations across multiple workspace packages causes configuration divergence, inconsistent test execution environments, and duplicated maintenance effort when updating shared runner settings or global test lifecycle rules.

## Decision

1. MUST: Global test environment lifecycle assertions and fixtures MUST use beforeAll and afterAll hooks imported directly from vitest.

## Policy Block

- MUST Global test environment lifecycle assertions and fixtures MUST use beforeAll and afterAll hooks imported directly from vitest.

In scope:
- Unit test suite configuration across all workspace packages
- Global test runner harness setup scripts and lifecycle hooks

Out of scope:
- End-to-end browser automation suites with independent runner runtimes
- Non-testing build or bundling configurations

## Rationale

- Composing test configurations through defineProject and mergeConfig ensures consistent test execution environments across all packages while accommodating package-specific overrides.
- Centralizing root options with defineConfig allows global test behavior adjustments without modifying individual package test definitions.
- Enforcing test lifecycle hooks such as beforeAll and afterAll from vitest guarantees uniform quality constraints across all test suites.

## Consequences

Positive:
- Eliminates configuration duplication across package test definitions.
- Ensures uniform test execution semantics and global assertion policies throughout the workspace.
- Simplifies maintenance by providing a single point of modification for shared test runner options.

Negative:
- Creates tight coupling between package test configurations and the root configuration interface.
- Requires package authors to understand configuration merging behavior to prevent unintended property overrides.

## Alternatives

- Independent standalone test configurations in each package (rejected)
  Rejected because: Causes test runner setting divergence and increases maintenance overhead across the workspace.
  When valid: When packages require entirely incompatible runtime environments or distinct testing frameworks.
- Single monolithic test configuration file for the entire workspace without package-level project definitions (rejected)
  Rejected because: Prevents packages from tailoring resolution paths, setup files, and test coverage scopes to their individual structures.
  When valid: When all workspace packages share identical directory structures, dependencies, and execution contexts.

## Risks

- Inadvertent property collisions during configuration merging causing unexpected test behavior
  Mitigation: Establish clear boundaries between shared base options and package-specific project overrides, verifying merged output via test execution.
  Owner: engineering team
- Base configuration updates breaking subproject test runner compatibility
  Mitigation: Validate all package test suites in continuous integration prior to merging shared test configuration changes.
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
- Base test runner configurations should be defined at the workspace root, exporting defaults that package configurations can import and combine using mergeConfig.
- Use defineProject within package directories to scope test execution targets and environment variables specifically for that package unit tests.

## Continuation Context


Verify commands:
- Discover the root test execution script from the project manifest and execute it to verify workspace test suites run cleanly.
- Discover package manifest test scripts and execute package-level test suites to confirm project configuration inheritance resolves properly.

Accept when:
- All package unit test suites execute and pass without configuration resolution errors.
- Configuration merging via mergeConfig resolves without conflicting property overrides or runtime schema warnings.
- Global test lifecycle hooks execute during suite setup and teardown as defined.

## Enforcement

- Verified by: Automated continuous integration pipeline executing unit test suites across all packages.
- Verified by: Code review checks validating that package test configurations use mergeConfig with base configuration imports.
- Violation handling: Pull requests with failing test suites or invalid test configuration resolution are blocked from merging.
- Violation handling: Test configurations that duplicate base settings instead of using inheritance must be refactored before approval.
- Exception process: Teams requiring divergent test runner configurations must submit an architectural review request explaining why base configuration inheritance cannot be used.