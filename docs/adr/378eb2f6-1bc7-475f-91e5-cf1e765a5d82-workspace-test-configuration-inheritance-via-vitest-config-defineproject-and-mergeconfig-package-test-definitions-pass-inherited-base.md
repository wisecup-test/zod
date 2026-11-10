---
version: 2
name: 378eb2f6-1bc7-475f-91e5-cf1e765a5d82-workspace-test-configuration-inheritance-via-vitest-config-defineproject-and-mergeconfig-package-test-definitions-pass-inherited-base
description: "Workspace Test Configuration Inheritance via vitest/config defineProject and mergeConfig: Package Test Definitions Pass Inherited Base"
metadata:
  actual:
    adr_id: 378eb2f6-1bc7-475f-91e5-cf1e765a5d82
    status: accepted
    candidate_group_id: 6efc0e41-02f6-440a-904f-b0bdbf205aab
    evidence:
      source: deep
  scope:
    root: packages/mini
---

# Workspace Test Configuration Inheritance via vitest/config defineProject and mergeConfig: Package Test Definitions Pass Inherited Base

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/mini`

Applies to:
- `**` (whole root)

## Context

- The repository contains modular workspace packages requiring localized unit test execution boundaries.
- Common test options and environment configurations must remain consistent across the codebase while allowing package-specific settings.
- Individual packages define their test projects by importing and merging base configurations using vitest/config capabilities.

## Problem Statement

Multi-package repositories risk configuration fragmentation and redundant maintenance when each package defines unit test parameters independently. A standardized mechanism is required to inherit baseline test settings while allowing workspace packages to declare project-level overrides.

## Decision

1. MUST: Package test definitions MUST pass the inherited base configuration into mergeConfig alongside package-specific settings to preserve repository-wide test defaults.

## Policy Block

- MUST Package test definitions MUST pass the inherited base configuration into mergeConfig alongside package-specific settings to preserve repository-wide test defaults.

In scope:
- Unit test configuration files located within workspace packages.
- Test suites requiring custom project-level overrides layered on top of shared base test settings.

Out of scope:
- Standalone external utility scripts that do not run within the workspace test harness.
- Integration or end-to-end testing environments managed by separate test infrastructure.

## Rationale

- Evidence demonstrates importing defineProject and mergeConfig from vitest/config to combine package-level definitions with a base configuration.
- Using mergeConfig ensures default execution options are retained rather than accidentally overwritten by partial project declarations.
- Standardizing on defineProject enables unified multi-project orchestration from the repository root.

## Consequences

Positive:
- Standardizes testing environment flags, plugins, and baseline rules across packages while permitting localized customization.
- Eliminates boilerplate duplication across individual package test configurations within the repository.
- Enables centralized test configuration updates that propagate consistently to all consuming packages.

Negative:
- Workspace packages become coupled to the structure and export format of the root test configuration artifact.
- Debugging test execution issues requires tracing configuration resolution between project overrides and inherited base settings.

## Alternatives

- Fully independent, unmerged test configurations per workspace package (rejected)
  Rejected because: Duplicates common test environment settings and execution flags across packages, creating configuration drift and maintenance overhead.
  When valid: Valid only when a package requires a completely disjoint runtime environment that cannot share root test settings.
- Single repository-root test configuration without project-level definitions (rejected)
  Rejected because: Prevents package-specific isolation, per-workspace test path filtering, and granular test execution boundaries.
  When valid: Valid in repositories with uniform source structures and identical test execution parameters across all files.

## Risks

- Modifications to the shared root test configuration may inadvertently break test execution in consuming packages.
  Mitigation: Execute complete workspace test runs during continuous integration before integrating root configuration changes.
  Owner: Engineering Team
- Incorrect merge ordering or conflicting properties in mergeConfig can lead to unpredictable test runner behavior.
  Mitigation: Standardize the argument order in mergeConfig so baseline settings are extended cleanly without clobbering essential options.
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
- Locate the root test configuration file relative to the package directory and ensure exported configuration objects remain compatible with mergeConfig.
- Configure package-level overrides strictly within defineProject to preserve multi-project execution capabilities across the workspace.

## Continuation Context


Verify commands:
- Discover and execute the project test runner script across all workspace packages to verify test configuration resolution.
- Discover and run the project static analysis or linting command to ensure compliance with test configuration import standards.

Accept when:
- Workspace test configuration files successfully import defineProject and mergeConfig from vitest/config to extend the base configuration.
- The repository verification suite executes all workspace unit tests without configuration resolution errors.

## Enforcement

- Verified by: Automated pull request validation pipelines running the test suite across all workspace packages.
- Verified by: Peer review checking compliance with vitest/config defineProject and mergeConfig adoption rules.
- Violation handling: Automated checks fail if package test configurations omit inheritance from the base test configuration.
- Violation handling: Pull requests introducing duplicated root configuration options or bypassing mergeConfig are blocked from merging.
- Exception process: Developers submit an architectural exception request detailing why the shared test configuration cannot satisfy package runtime requirements.
- Exception process: The proposed exception must be reviewed and approved by code maintainers before establishing a disconnected test configuration.