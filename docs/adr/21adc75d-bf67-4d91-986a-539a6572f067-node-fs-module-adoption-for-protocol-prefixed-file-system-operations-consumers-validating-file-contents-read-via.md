# node:fs Module Adoption for Protocol-Prefixed File System Operations: Consumers Validating File Contents Read Via

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Repository build scripts, code generators, and verification suites require direct file system access to parse configuration artifacts, validate version constraints, and emit package distributions.
- Legacy un-prefixed module specifiers create ambiguity between built-in runtime modules and external registry dependencies that might share identical package names.
- Static analysis across repository automation scripts detects uniform adoption of the protocol-prefixed node:fs module identifier alongside synchronous file reading APIs.
- Coordinated imports of complementary core utilities alongside node:fs substantiate a standardized approach to host environment interaction across workspace boundaries.

## Problem Statement

Unqualified module imports for host runtime services introduce vulnerability to dependency confusion and namespace collision when third-party packages mimic core utility names. Without a mandated protocol-prefixed import convention, repository build tools and verification scripts risk unpredictable module resolution behavior across disparate execution environments.

## Decision

1. MUST: Consumers validating file contents read via node:fs MUST enforce structured parsing and input validation before consuming data across package boundaries.

## Policy Block

- MUST Consumers validating file contents read via node:fs MUST enforce structured parsing and input validation before consuming data across package boundaries.

In scope:
- All repository build scripts, release automation, code generators, and static verification scripts performing file system operations.
- Workspace packages executing file generation or descriptor analysis.

Out of scope:
- Browser-targeted runtime bundles that do not execute within a host runtime environment containing native file system capabilities.
- Modules utilizing isolated virtual file system abstractions provided by testing harnesses.

Exceptions:
- EXC-20-001: A target deployment runtime strictly requires legacy module specifiers and lacks support for protocol-prefixed imports.

## Rationale

- Adopting explicit node:fs protocol specifiers guarantees that module resolution resolves directly to runtime built-ins, eliminating any risk of shadowing by packages in dependency manifests.
- Synchronous file access via readFileSync ensures sequential, predictable script execution during deterministic build and validation phases without asynchronous event loop overhead.
- Enforcing a uniform import standard across all four analyzed tooling and generation scripts establishes consistent repository maintenance practices across workspace boundaries.

## Consequences

Positive:
- Absolute immunity from dependency confusion attacks targeting bare core module specifiers.
- Immediate identification of runtime core dependencies during static code analysis and bundling.
- Consistent coding patterns across generation, verification, and packaging scripts.

Negative:
- Incompatibility with legacy execution runtimes that do not recognize protocol-prefixed module identifiers.
- Synchronous file system operations in node:fs block the main thread and are unsuitable for high-throughput runtime request pipelines.

## Alternatives

- Bare un-prefixed module specifiers for core file system operations (rejected)
  Rejected because: Leaves module resolution vulnerable to namespace squatting and relies on legacy resolution heuristics that obscure built-in origin.
  When valid: Valid only when maintaining compatibility with legacy execution environments preceding protocol scheme support.
- Third-party file system wrapper libraries (rejected)
  Rejected because: Adds unnecessary external dependencies and maintenance overhead when standard node:fs satisfies all repository tooling requirements.
  When valid: Valid when advanced abstractions like cross-platform virtual file systems or streaming pipelines are required.

## Risks

- Execution failures in legacy runtimes lacking support for protocol-prefixed imports.
  Mitigation: Ensure runtime environments declared in repository manifests meet minimum baseline specifications supporting protocol schemes.
  Owner: engineering team
- Unchecked exceptions during synchronous file reads causing script termination.
  Mitigation: Wrap readFileSync invocations in structured exception handlers and provide descriptive logging upon missing files or invalid content.
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
- Configure repository linting and static analysis rules to enforce the protocol prefix on all runtime core module imports.
- When processing file contents retrieved through readFileSync, enforce explicit character encoding and parse payload data within guarded blocks.

## Continuation Context


Verify commands:
- Discover the repository script runner and execute the module resolution linter to verify that all core imports utilize protocol prefixes.
- Discover and run the repository build validation script to ensure file system operations execute successfully across all target environments.

Accept when:
- Static analysis validates that every file system import across repository scripts utilizes the node:fs protocol specifier.
- All build generation and verification scripts complete without module resolution errors or unhandled file read exceptions.

## Enforcement

- Verified by: Automated static analysis checks in continuous integration pipelines.
- Verified by: Peer code review for pull requests modifying repository tooling and workspace generators.
- Violation handling: Continuous integration failure for any commit containing un-prefixed core module imports.
- Violation handling: Rejection of pull requests during automated static analysis verification.
- Exception process: Submit an architectural exception request documenting target environment constraints that prevent protocol prefix usage.
- Exception process: Obtain sign-off from the architecture review board and isolate legacy imports behind compatibility boundaries.