---
version: 2
name: 5aab3be0-09b3-453e-9173-c8aa67c5c96a-node-child-process-core-module-adoption-subprocess-management-in-automation-scripts-long-running-high-throughput-subprocesses-consume
description: "node:child_process Core Module Adoption: Subprocess Management in Automation Scripts: Long Running High Throughput Subprocesses Consume"
metadata:
  actual:
    adr_id: 5aab3be0-09b3-453e-9173-c8aa67c5c96a
    status: accepted
    candidate_group_id: 420288a8-2a72-4517-858a-135d93066c1f
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - .claude/skills/triage/scripts/**
      - scripts/**
---

# node:child_process Core Module Adoption: Subprocess Management in Automation Scripts: Long Running High Throughput Subprocesses Consume

Status: proposed
Date: 2025-05-14
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `.claude/skills/triage/scripts/**`
- `scripts/**`

## Context

- Repository maintenance scripts, triage tooling, and code verification routines require invoking external processes and system utilities
- Importing third-party process wrapper packages in developer scripts increases repository supply-chain surface area and dependency maintenance overhead
- Modern runtime environments provide built-in process execution capabilities via dedicated core modules accessible through explicit protocol specifiers

## Problem Statement

Automation and triage scripts requiring external command execution risk supply-chain bloat when relying on external wrapper libraries, or risk namespace resolution ambiguity when omitting explicit runtime protocol prefixes.

## Decision

1. SHOULD: Long-running or high-throughput subprocesses SHOULD consume output asynchronously via streams rather than buffering unbounded output in memory

## Policy Block

- SHOULD Long-running or high-throughput subprocesses SHOULD consume output asynchronously via streams rather than buffering unbounded output in memory

In scope:
- Repository automation scripts, maintenance utilities, and triage workflows executing external commands or system utilities

Out of scope:
- Client-side application code executing in browser environments where runtime process execution modules are unavailable

## Rationale

- Relying on the runtime core process module eliminates external package dependencies from repository maintenance scripts
- Explicit protocol prefixes prevent module resolution ambiguity and mitigate potential package confusion risks
- Direct subprocess primitives provide deterministic control over process lifecycles, exit statuses, and standard input and output streams

## Consequences

Positive:
- Zero third-party dependency footprint for repository maintenance and triage execution routines
- Deterministic process lifecycle control with transparent standard input, output, and error handling
- Unambiguous module resolution guaranteed by explicit protocol-prefixed specifiers

Negative:
- Low-level process spawning primitives require explicit stream handling and error code management compared to opinionated wrapper packages
- Operating system discrepancies in process invocation must be accounted for across developer environments

## Alternatives

- Adopt external process execution wrapper libraries from the package registry (rejected)
  Rejected because: Introduces third-party supply chain dependencies and maintenance overhead for repository scripts that only require standard subprocess invocation
  When valid: Complex multi-process orchestration pipelines with advanced cross-platform terminal formatting requirements
- Import runtime process capabilities via bare module specifiers (rejected)
  Rejected because: Bare module imports risk namespace collisions with registry packages and bypass explicit runtime resolution guarantees
  When valid: Legacy runtime environments that lack support for protocol-prefixed core module imports

## Risks

- Unchecked subprocess failures can result in silent script completion despite underlying execution errors
  Mitigation: Enforce explicit exit code inspection and standard error capture across all subprocess invocations
  Owner: engineering team
- Operating system behavioral differences in shell argument parsing can cause cross-platform execution failures
  Mitigation: Avoid shell string interpolation and pass arguments as discrete parameter arrays to process execution primitives
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
- Inspect the project dependency manifest to confirm runtime compatibility before utilizing newer core module functions
- Ensure process execution invocations capture exit codes and standard error output to provide clear diagnostic reporting on failure

## Continuation Context


Verify commands:
- Discover and execute the repository verification scripts declared in the root dependency manifest
- Discover and run static code inspection and typechecking suites across automation scripts to validate module import compliance

Accept when:
- All repository maintenance and triage scripts import process execution capabilities using the explicit protocol prefix
- Static validation and code inspection verification suites complete with zero errors across all repository scripts

## Enforcement

- Verified by: Automated continuous integration checks executing repository verification suites on every proposed change
- Verified by: Peer review validation of module imports and process error handling in all automation scripts
- Violation handling: Proposed changes containing bare module imports or unhandled process executions are rejected until brought into compliance
- Exception process: Exceptions require documented architectural justification and explicit review approval from repository maintainers