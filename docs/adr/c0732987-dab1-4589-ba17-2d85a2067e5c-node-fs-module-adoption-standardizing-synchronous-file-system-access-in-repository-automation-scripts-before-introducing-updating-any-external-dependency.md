---
version: 2
name: c0732987-dab1-4589-ba17-2d85a2067e5c-node-fs-module-adoption-standardizing-synchronous-file-system-access-in-repository-automation-scripts-before-introducing-updating-any-external-dependency
description: "node:fs Module Adoption: Standardizing Synchronous File System Access in Repository Automation Scripts: Before Introducing Updating Any External Dependency"
metadata:
  actual:
    adr_id: c0732987-dab1-4589-ba17-2d85a2067e5c
    status: accepted
    candidate_group_id: f60af43a-94a4-4f74-b47b-742a1e4db0fd
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - .claude/skills/triage/scripts/**
      - scripts/**
---

# node:fs Module Adoption: Standardizing Synchronous File System Access in Repository Automation Scripts: Before Introducing Updating Any External Dependency

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `.claude/skills/triage/scripts/**`
- `scripts/**`

## Context

- Repository automation, verification, and code generation scripts require direct access to the local file system to inspect metadata, verify consistency, and emit generated artifacts.
- Automation utilities observed across the repository consistently import file system capabilities directly from the runtime core namespace using protocol-qualified module specifiers rather than delegating to third-party file manipulation packages.
- Discrete scripting workflows execute sequentially during validation and triage pipelines, favoring deterministic synchronous read operations over asynchronous event loops where parallel non-blocking I/O is unnecessary.

## Problem Statement

Repository verification, code generation, and triage scripts must read and write repository configuration, schema artifacts, and documentation metadata without introducing extraneous third-party dependencies, conflicting namespace resolutions, or non-deterministic asynchronous execution paths during discrete build and validation workflows.

## Decision

1. MUST: Before introducing or updating any external dependency associated with repository tooling, engineers MUST inspect the project dependency manifest and lock artifact to resolve the exact locked version.

## Policy Block

- MUST Before introducing or updating any external dependency associated with repository tooling, engineers MUST inspect the project dependency manifest and lock artifact to resolve the exact locked version.

In scope:
- Standalone repository maintenance, triage, verification, and code generation scripts.
- Local file system inspection and artifact writing workflows executed outside of published distribution packages.

Out of scope:
- Runtime library source modules destined for cross-platform distribution where runtime-specific core module namespaces are unavailable.
- High-throughput asynchronous network server handlers requiring non-blocking streaming I/O.

## Rationale

- Adopting the core node:fs module with protocol-qualified specifiers eliminates unnecessary third-party dependencies for routine file system tasks and guarantees resolution from the native runtime core namespace.
- Utilizing synchronous operations like readFileSync within localized script executions provides deterministic, failure-fast execution without the boilerplate or race conditions of asynchronous orchestration.
- Enforcing explicit character encoding during file reads prevents platform-dependent default decoding issues when parsing structured configuration and source files.

## Consequences

Positive:
- Zero external dependencies are introduced for file system operations across maintenance and validation tooling.
- Deterministic linear execution in verification scripts simplifies debugging and diagnostics upon failure.
- Protocol-qualified module specifiers prevent accidental shadowing by identically named third-party packages.

Negative:
- Synchronous file operations block the execution thread, making them unsuitable for concurrent high-throughput workloads.
- Direct reliance on runtime core modules restricts execution to environments that provide compatible core module namespaces.

## Alternatives

- Adopting third-party file system utility packages for enhanced file manipulation (rejected)
  Rejected because: Third-party utility packages expand the dependency supply chain and introduce version drift risks for standard file read and write operations provided directly by runtime core modules.
  When valid: When complex recursive directory operations or cross-filesystem abstractions are required that native core modules do not provide.
- Mandating asynchronous file system APIs with promise-based handling across all script workflows (rejected)
  Rejected because: Asynchronous orchestration introduces unnecessary control flow complexity and boilerplate without providing meaningful performance gains in sequential single-threaded command-line scripts.
  When valid: When processing high volumes of files concurrently where I/O pipelining yields significant execution speedups.

## Risks

- Synchronous file reads on unexpectedly large files or slow file systems could block the runtime process.
  Mitigation: Limit synchronous reads to localized configuration, metadata, and generated source files, keeping data payloads bounded.
  Owner: Engineering Team
- Accidental usage of runtime-specific core modules in distribution packages intended for browser or edge environments.
  Mitigation: Enforce strict boundary separation between repository tooling scripts and published package distribution sources via automated linting.
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
- When reading structured data files, pass the text encoding parameter directly to readFileSync prior to parsing the decoded string.
- Wrap file system read operations in structured exception handling blocks to emit informative diagnostic messages upon file absence or access failure.

## Continuation Context


Verify commands:
- Discover the project verification script defined in the repository configuration manifest and execute it to verify repository integrity.
- Inspect script source files to confirm all file system imports utilize the protocol-prefixed core module namespace without third-party wrapper dependencies.

Accept when:
- All repository automation and verification scripts execute to completion without file system resolution errors.
- Static module import analysis confirms file system access in script files is restricted to the protocol-qualified core module namespace.

## Enforcement

- Verified by: Automated continuous integration checks that execute verification scripts on every pull request.
- Verified by: Static analysis and peer review of newly introduced or modified script files.
- Violation handling: Pull requests introducing third-party file system utilities or non-protocol-qualified imports in scripts will be blocked during review until updated to adhere to core module standards.
- Exception process: Exceptions require documented justification and approval from engineering leads where specialized third-party file manipulation features are demonstrably necessary.