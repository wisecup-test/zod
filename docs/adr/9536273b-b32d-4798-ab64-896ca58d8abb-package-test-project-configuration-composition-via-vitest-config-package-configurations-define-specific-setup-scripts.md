---
version: 2
name: 9536273b-b32d-4798-ab64-896ca58d8abb-package-test-project-configuration-composition-via-vitest-config-package-configurations-define-specific-setup-scripts
description: "Package Test Project Configuration Composition via vitest/config: Package Configurations Define Specific Setup Scripts"
metadata:
  actual:
    adr_id: 9536273b-b32d-4798-ab64-896ca58d8abb
    status: accepted
    candidate_group_id: 682b8cfd-bb53-4c8c-8bb2-12185574b204
    evidence:
      source: deep
  scope:
    root: packages/zod
---

# Package Test Project Configuration Composition via vitest/config: Package Configurations Define Specific Setup Scripts

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `**` (whole root)

## Context

- Multi-package workspace repositories require consistent unit test baselines across packages while accommodating package-level configuration divergence.
- Decoupled package testing requires isolated test project definitions that inherit shared workspace settings rather than duplicating test configurations.
- The codebase adopts vitest/config functions defineProject and mergeConfig to construct package test project configurations that extend the shared root configuration.

## Problem Statement

Maintaining independent unit test execution across workspace packages without configuration drift leads to either duplicated test runner settings or rigid monolithic configurations that fail to support package-specific requirements. The project requires a standardized mechanism to inherit global testing defaults while encapsulating package-specific test project boundaries.

## Decision

1. MAY: Package configurations MAY define package-specific setup scripts or custom test environment parameters when package runtime requirements diverge from the workspace baseline.

## Policy Block

- MAY Package configurations MAY define package-specific setup scripts or custom test environment parameters when package runtime requirements diverge from the workspace baseline.

In scope:
- Workspace packages requiring package-specific unit testing configurations within a multi-package repository.
- Test configurations that extend shared workspace baseline settings.

Out of scope:
- Root workspace configuration definitions establishing global test defaults.
- Single-package repositories without hierarchical configuration inheritance.

## Rationale

- Composing configurations using mergeConfig ensures that global testing updates in the root configuration propagate automatically across all packages.
- Declaring package test projects via defineProject enables workspace test runners to discover and execute package suites independently with isolated contexts.
- Centralizing common testing defaults prevents configuration divergence and reduces maintenance overhead across package boundaries.

## Consequences

Positive:
- Eliminates duplicate test runner settings across workspace package boundaries.
- Ensures consistent inheritance of common coverage thresholds, reporters, and runtime environments.
- Permits localized package test environment overrides without modifying global workspace defaults.

Negative:
- Creates coupling between package test configurations and the export shape of the root configuration.
- Requires developers to understand configuration merging semantics to avoid unintended property collisions or overwrites.

## Alternatives

- Independent standalone package test configurations without root inheritance (rejected)
  Rejected because: Duplicating testing configurations across packages causes maintenance overhead and configuration drift as baseline test requirements change.
  When valid: Valid when a package requires an isolated testing architecture completely incompatible with workspace defaults.
- Monolithic root test configuration without package-level project definitions (rejected)
  Rejected because: A single monolithic configuration prevents isolated package test environment specialization and granular per-package test execution.
  When valid: Valid in single-package repositories with uniform source structures and identical runtime requirements.

## Risks

- Modifications to the exported root configuration contract can break child package test project resolution.
  Mitigation: Validate root configuration changes against all package test projects in continuous integration before merging.
  Owner: engineering team
- Accidental deep override of merged properties could silently discard necessary root testing defaults.
  Mitigation: Establish automated test verification checks confirming merged configuration outputs retain required baseline settings.
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
- Import the shared root configuration via a relative path and pass it as the base configuration to mergeConfig alongside package-specific overrides.
- Ensure the resulting merged configuration object is exported using defineProject to support multi-project test orchestration.

## Continuation Context


Verify commands:
- find . -maxdepth 3 -type f -exec grep -l "defineProject" {} +
- find . -maxdepth 3 -type f -exec grep -l "mergeConfig" {} +
- REPO_ROOT=$(git rev-parse --show-toplevel 2>/dev/null || pwd) && grep -rn "from [\"']vitest/config[\"']" "$REPO_ROOT"

Accept when:
- Package test configuration modules import defineProject and mergeConfig from vitest/config.
- Package test project definitions compose the shared root configuration with package-specific overrides via mergeConfig.
- Project test verification directives execute package test suites without configuration composition errors.

## Enforcement

- Verified by: Automated continuous integration pipeline executing test suites across all workspace projects.
- Verified by: Static analysis checks verifying defineProject and mergeConfig imports in package configuration files.
- Verified by: Peer review on pull requests modifying test configuration definitions.
- Violation handling: Pull requests introducing unmerged or duplicate package test configurations are rejected during code review.
- Violation handling: Continuous integration failures resulting from invalid project configuration composition block merging.
- Exception process: Packages requiring an incompatible test runner paradigm must submit an architectural exception documenting why configuration inheritance cannot be used.
- Exception process: Exceptions require approval from repository maintainers and must be documented within the package directory.