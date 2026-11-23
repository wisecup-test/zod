---
version: 2
name: cross-cutting-modules-orchestrating-external-subproces-c19f
description: "Execa Subprocess Execution with SIGINT Interruption Lifecycle Cleanup: Modules Orchestrating External Subprocess Execution Use"
metadata:
  actual:
    adr_id: c19f1059-6c9d-4a38-be21-0c992998e095
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

# Execa Subprocess Execution with SIGINT Interruption Lifecycle Cleanup: Modules Orchestrating External Subprocess Execution Use

Scope: applies to `packages/tsc/bench/**`, `packages/tsc/bisect.ts`.

These rules are ALWAYS ACTIVE for:
- Modules and scripts that orchestrate asynchronous external subprocess executions
- CLI task runners and benchmarking harnesses managing long-running child processes

### Rules

- **R-IP-001** MUST: Modules orchestrating external subprocess execution MUST use execa for process invocation and MUST register a process.on signal handler for SIGINT events to manage child process lifecycles.

### Verify

- Discover and run the project static analysis and linting scripts to verify compliance with process execution and signal handler conventions.
- Discover and execute the project test runner against subprocess orchestration and signal handling test suites to confirm graceful termination.

**Accept when:**

- Subprocess executions use execa and register SIGINT signal listeners that terminate active child process handles.
- Interruption during execution results in all child processes being terminated without orphaned background tasks.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Static code analysis scanning for execa usage and associated SIGINT signal handler registrations
- Verified by: Automated test suites verifying process termination behavior during interruption signals
- Verified by: Peer code review for changes introducing external process execution
- Violation handling: Pull requests lacking required signal cleanup for spawned processes are blocked until lifecycle handlers are implemented.
- Violation handling: Automated linting failures flagging unhandled child process executions must be resolved before merging.
- Exception process: Exceptions for utilities requiring alternative lifecycle management must be documented with architectural review approval.
</enforcement>
