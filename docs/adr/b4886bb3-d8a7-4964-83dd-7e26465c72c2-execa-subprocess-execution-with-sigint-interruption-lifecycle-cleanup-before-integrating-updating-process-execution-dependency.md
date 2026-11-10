---
version: 2
name: b4886bb3-d8a7-4964-83dd-7e26465c72c2-execa-subprocess-execution-with-sigint-interruption-lifecycle-cleanup-before-integrating-updating-process-execution-dependency
description: "Execa Subprocess Execution with SIGINT Interruption Lifecycle Cleanup: Before Integrating Updating Process Execution Dependency"
metadata:
  actual:
    adr_id: b4886bb3-d8a7-4964-83dd-7e26465c72c2
    status: accepted
    candidate_group_id: e895d650-8efe-45bc-8e28-fbcfddc663a6
    evidence:
      source: deep
  scope:
    root: packages/tsc
    paths:
      - bench/**
      - bisect.ts
---

# Execa Subprocess Execution with SIGINT Interruption Lifecycle Cleanup: Before Integrating Updating Process Execution Dependency

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/tsc`

Applies to:
- `bench/**`
- `bisect.ts`

## Context

- Subprocess orchestration scripts require reliable process execution mechanisms to coordinate external compiler benchmarking and bisection workflows.
- Long-running asynchronous child processes can remain running in the background if the parent orchestrator is interrupted without propagating termination signals.
- The codebase adopts the execa library for process invocation while registering process event listeners on SIGINT signals to intercept termination requests and guarantee child process cleanup.

## Problem Statement

External process execution in long-running orchestration workflows risks creating orphaned child processes and dangling system resources when interruption signals are received, requiring a standardized execution mechanism and explicit signal lifecycle cleanup.

## Decision

1. MUST: Before integrating or updating the process execution dependency, developers MUST inspect the repository dependency manifest and lock artifact to verify the exact resolved dependency version and its documented process lifecycle APIs.

## Policy Block

- MUST Before integrating or updating the process execution dependency, developers MUST inspect the repository dependency manifest and lock artifact to verify the exact resolved dependency version and its documented process lifecycle APIs.

In scope:
- Modules and scripts that orchestrate asynchronous external subprocess executions
- CLI task runners and benchmarking harnesses managing long-running child processes

Out of scope:
- In-memory synchronous operations that do not spawn external system processes
- Short-lived purely internal utility functions with no subprocess boundaries

## Rationale

- Evidence across benchmarking and bisection modules demonstrates consistent adoption of execa alongside explicit process.on signal listener registration for SIGINT events.
- Direct child process termination via process handle iteration guarantees that external tasks do not linger as zombie or orphaned processes when a developer or automated runner terminates execution.
- Standardizing on execa provides consistent cross-platform process management while explicit signal event binding ensures deterministic cleanup across runtime boundaries.

## Consequences

Positive:
- Deterministic termination of child processes upon interruption prevents orphaned system processes and resource leaks.
- Unified subprocess execution interface provided by execa simplifies child process invocation and error handling.
- Explicit SIGINT interception ensures clean exit semantics across interactive and automated execution contexts.

Negative:
- Requires explicit tracking and state inspection of active child process handles within execution modules.
- Custom signal handling increases boilerplate in scripts that manage multiple concurrent processes.

## Alternatives

- Relying on default operating system process group signal propagation without explicit signal handlers (rejected)
  Rejected because: Default signal propagation can fail to kill detached or nested child processes, leaving orphaned background tasks consuming system resources.
  When valid: When child processes are attached synchronously to parent standard streams and guaranteed to terminate automatically upon parent exit.
- Standard language runtime child process spawning APIs without execa abstractions (rejected)
  Rejected because: Lower-level runtime process spawning lacks uniform cross-platform stream handling, buffer management, and ergonomic promise-based process lifecycle management.
  When valid: In minimal runtime environments where third-party dependencies are strictly prohibited.

## Risks

- Failure to clean up tracked process references after natural process completion could lead to memory retention in long-running orchestrators.
  Mitigation: Attach completion listeners to child processes to prune completed handles from the active process tracking collection.
  Owner: engineering team
- Throwing uncaught exceptions inside SIGINT signal listeners can bypass secondary cleanup logic or abort completion logging.
  Mitigation: Ensure signal listeners iterate through all tracked processes and log cleanup progress cleanly before exiting or re-throwing errors.
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
- Maintain a collection of running child process instances returned by execa and register a process.on listener for SIGINT to iterate and kill remaining active processes.
- Check the killed property on child process objects before issuing kill calls to avoid redundant termination signals on already-exited processes.

## Continuation Context


Verify commands:
- Discover and run the project static analysis and linting scripts to verify compliance with process execution and signal handler conventions.
- Discover and execute the project test runner against subprocess orchestration and signal handling test suites to confirm graceful termination.

Accept when:
- Subprocess executions use execa and register SIGINT signal listeners that terminate active child process handles.
- Interruption during execution results in all child processes being terminated without orphaned background tasks.

## Enforcement

- Verified by: Static code analysis scanning for execa usage and associated SIGINT signal handler registrations
- Verified by: Automated test suites verifying process termination behavior during interruption signals
- Verified by: Peer code review for changes introducing external process execution
- Violation handling: Pull requests lacking required signal cleanup for spawned processes are blocked until lifecycle handlers are implemented.
- Violation handling: Automated linting failures flagging unhandled child process executions must be resolved before merging.
- Exception process: Exceptions for utilities requiring alternative lifecycle management must be documented with architectural review approval.