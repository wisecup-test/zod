# Adopt @rollup/plugin-typescript for Bundler TypeScript Compilation: Developers Consult Repository Dependency Manifest Lock

Status: proposed
Date: 2025-05-14
Deciders: Detection Pipeline (automated)

## Context

- Repository build workflows require consistent compilation of TypeScript source code across shared configuration modules and individual package bundles.
- Module bundle configurations consistently integrate @rollup/plugin-typescript alongside resolution and bundle telemetry plugins to process typed modules.
- Relying on external or decoupled compilation passes introduces risk of configuration drift between type generation and bundled artifact emission.

## Problem Statement

Managing TypeScript compilation across multi-package repositories without a unified bundler plugin leads to inconsistent build outputs, fragmented source map generation, and desynchronized module transformations across build pipelines.

## Decision

1. MUST: Developers MUST consult the repository dependency manifest and lock artifact to resolve and verify the exact installed version of @rollup/plugin-typescript before modifying or extending bundling pipelines.

## Policy Block

- MUST Developers MUST consult the repository dependency manifest and lock artifact to resolve and verify the exact installed version of @rollup/plugin-typescript before modifying or extending bundling pipelines.

In scope:
- Build and bundle configurations compiling TypeScript source files across packages and shared modules.
- Configurations defining compilation pipelines for tree-shaking verification and package distribution.

Out of scope:
- Legacy JavaScript packages that do not contain TypeScript source code.
- Standalone test executions or static type-checking passes that run independently of artifact bundling.

## Rationale

- Integrating @rollup/plugin-typescript into the bundler plugin pipeline unifies compilation and bundling into a single coordinated pipeline, preventing mismatches between transpiled code and packaging.
- Evidence across repository configuration files demonstrates a consistent adoption pattern where TypeScript compilation operates directly within the module bundling lifecycle alongside resolution and sizing plugins.
- Centralizing TypeScript handling in the plugin layer reduces build configuration fragmentation across modular packages.

## Consequences

Positive:
- Ensures unified transpilation and type handling within bundler plugin pipelines across all adopting packages.
- Guarantees consistent source map alignment and module output formats across distribution targets.
- Streamlines build configurations by utilizing a standardized plugin pipeline for module resolution and compilation.

Negative:
- Couples TypeScript compilation throughput directly to the bundler execution lifecycle.
- Requires plugin updates to be coordinated with TypeScript compiler releases to maintain compatibility.

## Alternatives

- Two-stage compilation using a standalone TypeScript compiler followed by bundler packaging (rejected)
  Rejected because: Introduces intermediate filesystem artifacts, increases build latency, and complicates source map mapping between compilation stages.
  When valid: Valid when build pipelines strictly require declaration-only emission or when using non-bundler packaging systems.
- Adopting alternative transpilation plugins without integrated type checking (rejected)
  Rejected because: Lacks integrated type checking and declaration emission capabilities, requiring separate type verification passes.
  When valid: Valid in fast development watch modes where type checking is fully offloaded to an asynchronous background worker.

## Risks

- Compiler option mismatches between project configuration and bundler plugin settings
  Mitigation: Ensure plugin options align with repository-wide TypeScript configuration and inherit shared compilation settings.
  Owner: engineering team
- Build performance degradation on large codebases due to synchronous type checking in the bundle pipeline
  Mitigation: Tune plugin configuration to optimize declaration generation and leverage incremental compilation where supported.
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
- Discover the project configuration files to ensure the TypeScript plugin is ordered correctly with companion resolution and commonjs plugins in the pipeline array.
- Verify that module resolution options defined in repository compiler configurations are accurately propagated to the bundler plugin.

## Continuation Context


Verify commands:
- Discover the repository build script from the project manifest and execute the bundle build target to verify clean TypeScript compilation.
- Discover the test verification script from the project manifest and execute the test suite to validate that emitted bundle artifacts pass all functional checks.

Accept when:
- The module bundling process compiles TypeScript sources without diagnostic errors or missing declaration artifacts.
- Emitted bundles preserve accurate module exports and pass all automated verification checks defined in the repository.

## Enforcement

- Verified by: Automated continuous integration build checks validating successful artifact bundling.
- Verified by: Peer code review verifying that new or modified bundle configurations integrate the required plugin.
- Violation handling: Build failures in continuous integration pipelines if bundle generation fails or unauthorized compilation flows are introduced.
- Violation handling: Pull request rejection during code review for configurations that bypass the standardized plugin pipeline.
- Exception process: Submit an architectural review request detailing the technical constraint preventing the use of the standardized plugin, accompanied by an alternative compilation plan and team lead approval.