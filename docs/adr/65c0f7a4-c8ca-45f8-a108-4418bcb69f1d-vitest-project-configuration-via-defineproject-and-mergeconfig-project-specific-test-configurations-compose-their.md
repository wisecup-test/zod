---
version: 2
name: 65c0f7a4-c8ca-45f8-a108-4418bcb69f1d-vitest-project-configuration-via-defineproject-and-mergeconfig-project-specific-test-configurations-compose-their
description: "Vitest Project Configuration via defineProject and mergeConfig: Project Specific Test Configurations Compose Their"
metadata:
  actual:
    adr_id: 65c0f7a4-c8ca-45f8-a108-4418bcb69f1d
    status: accepted
    candidate_group_id: 3df92587-e67c-4c97-9ee1-b9c7703662f4
    evidence:
      source: deep
  scope:
    root: packages/docs
---

# Vitest Project Configuration via defineProject and mergeConfig: Project Specific Test Configurations Compose Their

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `**` (whole root)

## Context

- Multi-package codebases require consistent test runner semantics across distinct packages while accommodating package-specific environment requirements.
- Centralized root test configurations define base runtime flags, coverage reporters, and execution thresholds that should apply uniformly across sub-projects.
- Direct duplication of test configuration across individual packages causes configuration drift, maintenance overhead, and divergent test behaviors.
- The codebase introduces module-level project test definitions using vitest/config integration points to derive package configurations from a shared root configuration.

## Problem Statement

Uncoordinated test configurations across sub-packages lead to fragmented testing standards, duplicate boilerplate, and inconsistent execution semantics across workspace boundaries.

## Decision

1. MUST: Project-specific test configurations MUST compose their settings with the shared root test configuration using mergeConfig from vitest/config rather than redefining global execution parameters independently.

## Policy Block

- MUST Project-specific test configurations MUST compose their settings with the shared root test configuration using mergeConfig from vitest/config rather than redefining global execution parameters independently.

In scope:
- Unit and integration test configuration across individual workspace packages.
- Sub-project test definitions inheriting from shared repository-level test configurations.

Out of scope:
- Repository root-level test suite orchestration and global runner entry points.
- Non-unit test workflows governed by standalone external runners.

Exceptions:
- EXC-39-001: A package requires an isolated execution environment incompatible with root configuration flags.

## Rationale

- Hierarchical configuration composition via mergeConfig and defineProject prevents configuration drift across distinct packages while maintaining a single source of truth for global test execution parameters.
- Standardizing on vitest/config APIs provides native support for multi-project test orchestration, allowing individual packages to be executed in isolation or aggregated into comprehensive workspace runs.
- Encapsulating package overrides within explicit project definitions preserves root governance over quality gates, reporting formats, and execution rules.

## Consequences

Positive:
- Ensures uniform test execution semantics, reporter formats, and coverage criteria across workspace packages.
- Minimizes duplicate boilerplate across package test configuration modules.
- Facilitates seamless localized package test runs as well as unified whole-repository test runs.

Negative:
- Creates structural coupling between package-level test configuration modules and the relative path of the shared root configuration.
- Upstream changes to root configuration defaults risk propagating unintended test behavioral shifts across dependent sub-projects.

## Alternatives

- Autonomous Package Test Configurations (rejected)
  Rejected because: Duplicating complete configuration objects in every package results in configuration drift, inconsistent quality thresholds, and elevated maintenance overhead.
  When valid: Valid only in standalone, decoupled repositories containing a single isolated module.
- Monolithic Root Configuration Without Sub-Project Definitions (rejected)
  Rejected because: A single global configuration file lacks the flexibility to apply package-specific setup routines, environment variables, or module resolution rules required by diverse workspace components.
  When valid: Valid in uniform codebases where every sub-component shares identical test execution environments.

## Risks

- Breaking changes in inherited root configuration can silently alter or fail test execution across multiple packages simultaneously.
  Mitigation: Validate root configuration modifications against all workspace sub-project test suites in automated continuous integration prior to merging.
  Owner: Quality Engineering / Infrastructure Team
- Relative path resolution between package configurations and root configuration modules may break during package directory reorganization.
  Mitigation: Establish linting rules or path resolution checks that verify relative inheritance links during repository integrity scans.
  Owner: Core Platform Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Import defineProject and mergeConfig from vitest/config in each sub-package configuration module, merging local overrides into the imported root base configuration object.
- Keep package-level test configuration focused exclusively on package-specific setup routines and environment flags, delegating runner, reporter, and threshold defaults to the shared root module.

## Continuation Context


Verify commands:
- Discover the repository test execution script from the workspace root manifest and execute the workspace-wide test suite to confirm all project configurations resolve and pass.
- Discover the repository configuration linting script from the workspace root manifest and execute it to verify conformance of all sub-project test configuration files.

Accept when:
- All sub-package test configurations successfully merge the shared root configuration without schema validation errors during test initialization.
- The workspace test runner discovers and executes tests across all configured sub-projects with unified reporting output.

## Enforcement

- Verified by: Automated continuous integration pipeline execution verifying project test configuration resolution.
- Verified by: Peer code review for all modifications to sub-package test configuration files.
- Violation handling: Pull requests containing unmerged, duplicate standalone configurations without documented approval are blocked from merging.
- Violation handling: Static analysis warnings or build failures triggered by invalid project configuration schemas.
- Exception process: Submit an architectural review request outlining package-specific technical constraints that necessitate divergence from root test configuration.