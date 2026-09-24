# execa Process Execution Library Adoption: Consumer Inspect Repository Lock Resolution Artifact

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Multiple performance benchmarking, bisecting, and resolution verification modules require programmatic execution of external processes and script targets.
- Spawning external processes without standardized abstraction introduces inconsistencies in stream management, exit code handling, and asynchronous promise integration.
- Long-running or iterative child executions risk leaving orphaned processes upon interruption unless signal listeners explicitly track and terminate child instances.

## Problem Statement

Automated benchmark runners, bisection scripts, and resolution verification tools must execute child processes while maintaining structured promise resolution, standard stream management, and clean process lifecycle termination during abort signals.

## Decision

1. MUST: The consumer MUST inspect the repository lock or resolution artifact to determine the exact resolved version of execa prior to implementation, verifying that all invoked APIs conform to that exact version reference.

## Policy Block

- MUST The consumer MUST inspect the repository lock or resolution artifact to determine the exact resolved version of execa prior to implementation, verifying that all invoked APIs conform to that exact version reference.

In scope:
- Benchmarking suites, bisection tools, and resolution verification scripts that spawn external commands or helper modules.
- Utility scripts that manage concurrent or sequential child process execution lifecycles.

Out of scope:
- Pure computational libraries, unit test suites, and modules that do not invoke child processes.
- In-process module loading or direct programmatic evaluation where process boundaries are unnecessary.

Exceptions:
- EXC-20-001: A specialized runtime environment restricts external library execution and requires native runtime process primitives.

## Rationale

- Adopting execa provides promise-based process invocation, automatic stream handling, and predictable exit code propagation across diagnostic and benchmarking routines.
- Pairing execa with centralized signal handlers eliminates orphaned processes during early cancellation or execution failures.
- Consolidating child process execution to a single library across nine diagnostic modules prevents fragmented subprocess invocation patterns across the repository.

## Consequences

Positive:
- Uniform asynchronous process execution and structured error propagation across benchmarking and verification tooling.
- Guaranteed child process termination during interruption signals, preventing resource leaks and orphaned processes.
- Simplified maintenance through consistent standard input-output stream piping and exit status parsing.

Negative:
- Introduces an external dependency that must be maintained and tracked across repository lock artifacts.
- Requires explicit signal handling overhead in tooling scripts to ensure process instance cleanup.

## Alternatives

- Built-in runtime child process primitives without external wrappers (rejected)
  Rejected because: Native child process primitives require verbose boilerplate for promise conversion, stream aggregation, and cross-platform process termination.
  When valid: When zero-dependency execution is strictly mandated by the runtime environment.
- Synchronous process execution helpers (rejected)
  Rejected because: Synchronous process execution blocks the main event loop and prevents graceful signal handling during long-running benchmark or bisect loops.
  When valid: When executing non-blocking, trivial inspection commands that run in negligible time.

## Risks

- Untracked child process handles during sudden parent process termination could leave orphan processes consuming system resources.
  Mitigation: Track active process references in a collection and register interruption event handlers to kill running instances upon signal reception.
  Owner: Tooling and Infrastructure Engineering
- Breaking API changes across major library versions if updated without version grounding.
  Mitigation: Adhere to the lock-version grounding policy by verifying resolved lock artifact versions and public API documentation before adopting new method signatures.
  Owner: Tooling and Infrastructure Engineering

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Maintain an internal registry or collection of active child process references within long-running automation scripts so that signal handlers can iterate and terminate outstanding processes.
- Handle standard stream outputs using asynchronous promise interfaces to capture errors and output without blocking runtime execution.

## Continuation Context


Verify commands:
- Discover and run the project's static analysis and dependency verification scripts to confirm execa import compliance.
- Discover and run the project's automated test suite to ensure benchmarking and verification scripts execute and terminate child processes cleanly.

Accept when:
- All subprocess invocations within tooling and benchmark modules import and use execa.
- Process execution scripts register interruption handlers that successfully terminate active child processes upon signal dispatch.
- Project verification suites pass without unhandled child process rejections or zombie processes.

## Enforcement

- Verified by: Automated linting and static analysis checks validating library import constraints.
- Verified by: Continuous integration pipeline test runs validating benchmark execution and clean process termination.
- Verified by: Peer review for all modifications to child process invocation logic.
- Violation handling: Pull requests introducing unapproved subprocess mechanisms or omitting signal cleanup will be blocked until refactored.
- Violation handling: Violating code must be updated to use execa with proper process tracking before merge.
- Exception process: Submit an architectural variance request detailing why standard process spawning is unsuitable.
- Exception process: Obtain formal approval from the architecture review group and document custom lifecycle handling in the module.