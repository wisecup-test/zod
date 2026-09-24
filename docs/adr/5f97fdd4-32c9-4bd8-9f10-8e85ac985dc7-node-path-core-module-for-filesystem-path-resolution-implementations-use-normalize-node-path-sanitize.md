# node:path Core Module for Filesystem Path Resolution: Implementations Use Normalize Node Path Sanitize

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Tooling scripts, test runners, and workspace packages require consistent cross-platform filesystem path resolution and file navigation.
- Modular repository architectures separating build configuration, workspace resolution checks, and maintenance workflows encounter platform-specific path separator and resolution discrepancies if string concatenation is used.
- The codebase standardizes on explicit protocol-prefixed core module imports, notably node:path alongside companion URL resolution modules, to guarantee unambiguous module loading and deterministic path calculation.

## Problem Statement

Inconsistent filesystem path resolution across repository maintenance scripts, configuration modules, and test suites leads to runtime failures across disparate operating systems and introduces ambiguous module resolution when core modules are imported without explicit namespace prefixes.

## Decision

1. MAY: Implementations MAY use normalize from node:path to sanitize user-provided or externally sourced relative path inputs before resolution.

## Policy Block

- MAY Implementations MAY use normalize from node:path to sanitize user-provided or externally sourced relative path inputs before resolution.

In scope:
- All repository maintenance scripts, configuration definitions, and test suites executing in the project environment.
- Any workspace component or utility module requiring filesystem path creation, navigation, or verification.

Out of scope:
- Browser-only client runtime code that executes in environments where filesystem APIs do not exist.
- Pure algorithmic code operating exclusively on in-memory data structures without filesystem interaction.

## Rationale

- Explicit protocol-prefixed specifiers prevent namespace collision between core runtime modules and third-party packages, ensuring predictable resolution across execution contexts.
- Systematic path manipulation through node:path APIs guarantees uniform behavior across diverse host operating systems, preventing separator and normalization bugs.
- Consistent module imports observed across five critical repository scripts and configuration files establish a repository-wide convention that maintains codebase cohesion and portability.

## Consequences

Positive:
- Eliminates platform-specific filesystem bugs caused by disparate path separators.
- Disambiguates runtime core module resolution by strictly utilizing protocol-prefixed specifiers.
- Provides predictable module-relative directory calculation across configuration and automation scripts.

Negative:
- Requires explicit conversion between file URLs and system paths when operating in module configurations.
- Precludes direct execution in browser environments without polyfills or bundling shims.

## Alternatives

- Legacy un-prefixed core module imports (rejected)
  Rejected because: Un-prefixed imports risk collision with userland packages during dependency resolution and lack modern namespace clarity.
  When valid: Valid only in legacy execution runtimes that do not support protocol-prefixed module resolution.
- Third-party cross-platform path utilities (rejected)
  Rejected because: Introduces unnecessary external dependencies and maintenance overhead when the built-in core module provides standard path operations.
  When valid: Valid when specialized path manipulation capabilities not provided by the core runtime are explicitly required.

## Risks

- Inadvertent inclusion of node:path in client-facing bundles causing build or runtime failures.
  Mitigation: Enforce build boundary checks and static analysis rules preventing core module imports within client target boundaries.
  Owner: engineering team
- Mismatched path normalization between Windows backslashes and POSIX forward slashes in string comparisons.
  Mitigation: Standardize on normalize or posix sub-path APIs when performing normalized string comparisons across operating systems.
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
- Ensure all module specifiers utilize the protocol prefix when accessing core runtime modules.
- When resolving paths relative to current module files, convert module location URLs to system paths prior to passing them into path calculation methods.

## Continuation Context


Verify commands:
- Discover and execute the repository test suite through the configured test runner script in the project manifest.
- Run the project static analysis and linting verification scripts to check for un-prefixed core module imports.
- Execute the project build and resolution scripts to verify cross-platform path resolution across workspace packages.

Accept when:
- All repository test suites and verification scripts pass without path resolution errors.
- Static analysis confirms zero un-prefixed core module imports across repository scripts and configurations.
- Path resolution tests succeed consistently across both POSIX and Windows runtime environments.

## Enforcement

- Verified by: Continuous integration pipelines executing repository verification and test scripts.
- Verified by: Static analysis and linting rules prohibiting un-prefixed core module imports.
- Verified by: Peer code review for pull requests modifying tooling or configuration modules.
- Violation handling: Automated pull request checks fail if un-prefixed imports or non-portable path operations are detected.
- Violation handling: Pull requests containing hardcoded directory separators or string path concatenations are blocked until remediated.
- Exception process: Submit an architectural review request documenting technical constraints preventing protocol-prefixed import usage.
- Exception process: Obtain explicit approval from repository maintainers before merging any approved deviation.