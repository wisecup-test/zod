# Hierarchical Test Configuration Composition Using vitest/config: Composed Configuration Result Wrapped Exported Defineconfig

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- The repository organizes code into monorepo workspace packages requiring consistent unit test execution.
- Duplicating test runner settings across individual packages introduces maintenance overhead and configuration drift.
- Package-level test suites require shared defaults while preserving the ability to define package-specific options.
- The codebase establishes inheritance by importing defineConfig and mergeConfig from vitest/config to combine package configurations with a root configuration.

## Problem Statement

Maintaining independent unit test runner configurations across multiple workspace packages risks diverging execution environments, inconsistent reporter setups, and duplicate boilerplate. A standardized mechanism is required to inherit base test execution defaults across packages while allowing package-specific customizations without breaking consistency.

## Decision

1. MUST: The composed configuration result MUST be wrapped and exported using defineConfig from vitest/config.

## Policy Block

- MUST The composed configuration result MUST be wrapped and exported using defineConfig from vitest/config.

In scope:
- Unit test runner configurations for workspace packages within the repository.
- Test runner setup modules extending repository-wide test execution settings.

Out of scope:
- End-to-end or external integration test suites governed by separate runner configurations.
- Standalone single-package repositories without monorepo workspace boundaries.

## Rationale

- Using mergeConfig and defineConfig from vitest/config enables deep configuration merging between shared base test settings and package-specific overrides.
- Centralizing common test execution rules in a shared root configuration module eliminates boilerplate across packages and simplifies repository-wide updates.
- Package-level configuration isolation ensures that individual workspace packages can customize test discovery and environment details without altering global settings.

## Consequences

Positive:
- Consistent test execution defaults and reporters across all workspace packages.
- Reduced configuration duplication and lower maintenance burden across monorepo boundaries.
- Package-specific test requirements can be accommodated safely via explicit mergeConfig overrides.

Negative:
- Package configurations are coupled to the relative path and interface of the shared root configuration module.
- Deep merging via mergeConfig can lead to subtle override interactions if base options are modified without cross-package testing.

## Alternatives

- Independent standalone test configurations in each workspace package without root sharing (rejected)
  Rejected because: Results in widespread duplication of test runner options and configuration drift across packages.
  When valid: Valid only in decoupled repositories with completely disparate testing frameworks and runtimes.
- Single monolithic root test configuration running all workspace tests without per-package configuration files (rejected)
  Rejected because: Prevents individual packages from customizing package-specific test filters, environment mocks, or isolated execution settings.
  When valid: Valid in small repositories with completely uniform packages and no package-specific testing needs.

## Risks

- Changes to the shared root configuration module could unintentionally break unit test execution in downstream packages.
  Mitigation: Run workspace-wide test verification in continuous integration whenever the root configuration module is modified.
  Owner: engineering team
- Deep merging via mergeConfig may unintentionally overwrite array options or nested objects in unexpected ways.
  Mitigation: Review package configuration overrides and inspect resolved configurations during setup changes.
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
- Import defineConfig and mergeConfig from vitest/config alongside the shared root test configuration when creating package-level test configuration modules.
- Ensure that package-specific overrides passed to mergeConfig supply only the delta needed for the package test suite.

## Continuation Context


Verify commands:
- Discover and run the repository test execution script declared in the root dependency manifest across all workspace packages.
- Execute the workspace-specific test script for the target package to verify that merged configuration loads and executes tests successfully.

Accept when:
- The package test runner successfully loads the merged configuration from vitest/config without runtime errors.
- All unit tests in the workspace package execute and pass using the inherited and package-specific configuration options.

## Enforcement

- Verified by: Automated continuous integration test execution verifying all workspace packages.
- Verified by: Pull request code reviews examining package test configuration modules.
- Violation handling: Pull requests introducing unmerged or duplicate standalone test configurations will be blocked during review.
- Violation handling: Test execution failures in continuous integration resulting from invalid configuration composition will prevent merging.
- Exception process: Exceptions for packages requiring fundamentally distinct test runner frameworks require approval from the architecture team with documented architectural justification.