---
version: 2
name: 806ea227-7a7f-4e6a-865c-923690bbb0ad-node-protocol-core-modules-adoption-explicit-namespace-protocol-resolution-for-core-runtime-utilities-source-modules-configuration-units-repository-utility
description: "node: Protocol Core Modules Adoption: Explicit Namespace Protocol Resolution for Core Runtime Utilities: Source Modules Configuration Units Repository Utility"
metadata:
  actual:
    adr_id: 806ea227-7a7f-4e6a-865c-923690bbb0ad
    status: accepted
    candidate_group_id: b221aea1-37c8-4893-8cb2-d3c57617eb2f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
      - vitest.compile.config.ts
      - vitest.config.ts
      - vitest.root.mjs
---

# node: Protocol Core Modules Adoption: Explicit Namespace Protocol Resolution for Core Runtime Utilities: Source Modules Configuration Units Repository Utility

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `scripts/**`
- `vitest.compile.config.ts`
- `vitest.config.ts`
- `vitest.root.mjs`

## Context

- Runtime environments provide built-in core utility modules for handling fundamental system capabilities including filesystem operations, path normalization, and URL parsing.
- Bare module specifiers introduce namespace ambiguity between built-in runtime modules and external third-party registry packages, exposing codebases to dependency shadowing and resolution conflicts.
- Analysis of configuration files and repository automation scripts across the codebase demonstrates uniform adoption of protocol-prefixed module specifiers for core system utilities.

## Problem Statement

Relying on bare module specifiers for core runtime functionality allows third-party packages to shadow system modules, introduces ambiguity in ECMAScript module resolution pipelines, and prevents static tooling from deterministically distinguishing between internal platform interfaces and external dependencies.

## Decision

1. MUST_NOT: Source modules, configuration units, and repository utility scripts MUST NOT import runtime core utilities using un-prefixed bare specifiers.

## Policy Block

- MUST_NOT Source modules, configuration units, and repository utility scripts MUST NOT import runtime core utilities using un-prefixed bare specifiers.

In scope:
- All repository configuration files requiring core system utilities
- All automation and verification scripts interfacing with filesystem, path, or URL capabilities
- All internal modules relying on runtime platform interfaces

Out of scope:
- Client-side browser application bundles executing in environments lacking runtime core module support
- Third-party vendor libraries packaged as external distribution artifacts

## Rationale

- Explicit protocol prefixes prevent dependency confusion and typosquatting attacks by enforcing deterministic resolution to platform core modules rather than registry packages.
- Protocol-prefixed imports conform to standardized ECMAScript module specifications, ensuring predictable static analysis and compatibility across modern execution runtimes.
- Uniform usage across all configuration definitions and maintenance scripts creates an unambiguous boundary between platform capabilities and third-party dependencies.

## Consequences

Positive:
- Eliminates namespace collisions and prevents malicious or accidental shadowing of platform modules by third-party packages.
- Enables static analysis and bundlers to immediately recognize platform built-ins without heuristic resolution checks.
- Ensures consistency across configuration files, maintenance scripts, and automation tasks.

Negative:
- Precludes execution on legacy runtime versions that do not support protocol-prefixed specifiers without transformation.
- Requires automated linting and continuous integration checks to prevent regression to legacy bare specifiers.

## Alternatives

- Permit legacy bare module specifiers without protocol prefixes for runtime core utilities (rejected)
  Rejected because: Bare specifiers risk dependency shadowing, conflict with third-party registry packages, and create ambiguity in static analysis tooling
  When valid: Only valid when targeting legacy runtime environments that lack protocol prefix support and cannot run module transformation steps
- Encapsulate core utility interactions inside a custom internal abstraction wrapper (rejected)
  Rejected because: Adds unnecessary indirection and maintenance overhead for standard platform capabilities already standardized by the runtime
  When valid: Valid when multi-runtime polyfilling across incompatible platform environments is strictly required

## Risks

- Developers unintentionally introduce bare specifiers in new scripts or configuration modules
  Mitigation: Enforce static analysis linting rules in automated continuous integration to reject un-prefixed core module imports
  Owner: engineering team
- External tooling or legacy execution runners fail to resolve protocol-prefixed specifiers
  Mitigation: Ensure all execution runtimes and build tools conform to the resolved versions specified in the repository lock artifact
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
- Configure the repository static analysis linter to enforce protocol-prefixed specifiers for all imports of path, filesystem, and URL runtime modules.
- Verify that build and test execution pipelines run against runtimes that natively support protocol-prefixed module resolution.

## Continuation Context


Verify commands:
- Discover and run the repository linter to verify that no bare imports of runtime core modules exist in source or configuration files.
- Discover and run the repository test and type-checking scripts to verify successful resolution of all protocol-prefixed module imports.

Accept when:
- Static analysis and linting pass with zero violations of core module import prefix rules.
- All test suites and configuration modules execute and resolve runtime core utilities without resolution errors.

## Enforcement

- Verified by: Automated continuous integration lint checks inspecting import specifiers
- Verified by: Code review validation for all new configuration files and utility scripts
- Violation handling: Pull requests containing bare specifiers for runtime core modules are blocked by automated continuous integration
- Violation handling: Violations must be updated to use the explicit protocol prefix before merge approval
- Exception process: Exceptions for legacy compatibility require written justification and approval from the lead architecture maintainers.