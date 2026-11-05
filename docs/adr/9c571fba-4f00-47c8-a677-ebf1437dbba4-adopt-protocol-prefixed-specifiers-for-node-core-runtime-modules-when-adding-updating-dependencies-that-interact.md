---
version: 2
name: 9c571fba-4f00-47c8-a677-ebf1437dbba4-adopt-protocol-prefixed-specifiers-for-node-core-runtime-modules-when-adding-updating-dependencies-that-interact
description: "Adopt Protocol-Prefixed Specifiers for Node Core Runtime Modules: When Adding Updating Dependencies That Interact"
metadata:
  actual:
    adr_id: 9c571fba-4f00-47c8-a677-ebf1437dbba4
    status: accepted
    candidate_group_id: be88ca21-c354-4c2a-953c-43d58c347707
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/resolution/**
      - scripts/**
      - vitest.config.ts
      - vitest.root.mjs
---

# Adopt Protocol-Prefixed Specifiers for Node Core Runtime Modules: When Adding Updating Dependencies That Interact

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `packages/resolution/**`
- `scripts/**`
- `vitest.config.ts`
- `vitest.root.mjs`

## Context

- Core execution scripts, workspace resolution verification tests, and test runner configurations consistently utilize the node: protocol namespace when importing built-in runtime capabilities such as path, url, and filesystem modules.
- Modern JavaScript and TypeScript runtimes support explicit protocol-prefixed specifiers to differentiate built-in platform APIs from third-party registry packages.
- Consistently using explicit protocol prefixes eliminates module resolution ambiguity across CommonJS and ES module environments.

## Problem Statement

Importing built-in runtime capabilities using bare specifiers introduces resolution ambiguity between standard library modules and potential third-party packages, while increasing the risk of module shadowing in package resolution.

## Decision

1. MUST: When adding or updating dependencies that interact with runtime core modules, the consumer MUST discover the repository lock artifact and verify resolved versions against the dependency manifest before implementing changes.

## Policy Block

- MUST When adding or updating dependencies that interact with runtime core modules, the consumer MUST discover the repository lock artifact and verify resolved versions against the dependency manifest before implementing changes.

In scope:
- All TypeScript and JavaScript source files, maintenance scripts, and runner configurations that reference runtime core modules.

Out of scope:
- Third-party registry packages or internal workspace package specifiers that do not belong to the runtime standard library.

## Rationale

- Evidence across multiple script files, runner configurations, and resolution tests demonstrates uniform adoption of node: protocol specifiers for core platform imports.
- Explicit protocol prefixing provides unambiguous module resolution, security against dependency confusion, and explicit intent across both ES module and CommonJS execution contexts.

## Consequences

Positive:
- Guarantees deterministic resolution of core runtime capabilities without risk of registry package shadowing.
- Maintains clear visual and semantic separation between runtime-native capabilities and external third-party dependencies.
- Ensures full compatibility with modern ES module resolution algorithms and tooling across scripts and test configs.

Negative:
- Requires strict adherence to protocol prefixes across all development and tooling scripts.
- Incompatible with obsolete execution environments that lack native protocol resolution capabilities.

## Alternatives

- Bare specifier imports for runtime core modules (rejected)
  Rejected because: Bare specifiers create ambiguity between built-in modules and potential userland dependencies in external package registries, and lack explicit protocol scoping.
  When valid: Only valid in legacy runtime environments that do not support protocol-prefixed core module imports.
- Ad-hoc mixing of bare specifiers and protocol-prefixed specifiers (rejected)
  Rejected because: Inconsistent specifier usage leads to fragmented codebase conventions and complicates automated import linting rules.
  When valid: Never valid within a modern module boundary where protocol imports are fully supported.

## Risks

- Execution in an outdated runtime environment that lacks support for protocol-prefixed module imports.
  Mitigation: Enforce minimum runtime engine compatibility checks during build and execution workflows.
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
- Configure import linting rules in the project's static analysis configuration to automatically flag and autofix un-prefixed runtime core module imports.
- Ensure all configuration files and standalone scripts align with the protocol namespace convention used in runtime and test runners.

## Continuation Context


Verify commands:
- Discover the project's automated verification script from the dependency manifest and run the linter to ensure no un-prefixed core imports exist.
- Discover and execute the project's test suite to verify module resolution succeeds across all configurations.

Accept when:
- All workspace modules and scripts import core Node.js runtime facilities exclusively using the node: protocol namespace prefix.
- Static analysis and automated lint checks verify zero un-prefixed standard library module specifiers exist across the codebase.
- Test suites and build verification scripts execute without module resolution ambiguities or warnings.

## Enforcement

- Verified by: Automated code linting rules configured to enforce protocol prefixes on runtime core imports.
- Verified by: Continuous integration verification runs across all configuration files and utility scripts.
- Violation handling: Pull requests containing un-prefixed core module specifiers fail automated linting and must be updated before merging.
- Exception process: Exceptions require architectural review and must document specific legacy platform constraints necessitating bare module specifiers.