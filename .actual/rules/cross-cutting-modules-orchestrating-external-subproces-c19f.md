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

These rules are ALWAYS ACTIVE for modules and scripts that orchestrate asynchronous external subprocess executions, CLI task runners, and benchmarking harnesses managing long-running child processes.

### Rules

- **R-EXEC-001** MUST: Modules orchestrating external subprocess execution MUST use execa for process invocation.
- **R-EXEC-002** MUST: Modules orchestrating external subprocess execution MUST register a process.on signal handler for SIGINT events to manage child process lifecycles.
- **R-EXEC-003** MUST: Maintain a collection of running child process instances returned by execa and register a process.on listener for SIGINT to iterate and kill remaining active processes.
- **R-EXEC-004** MUST: Check the killed property on child process objects before issuing kill calls to avoid redundant termination signals on already-exited processes.
- **R-EXEC-005** MUST: Attach completion listeners to child processes to prune completed handles from the active process tracking collection to prevent memory retention.
- **R-EXEC-006** MUST: Ensure signal listeners iterate through all tracked processes and log cleanup progress cleanly before exiting or re-throwing errors to avoid bypassing secondary cleanup logic.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify compliance with process execution and signal handler conventions.
npm run lint || yarn lint

# Discover and execute the project test runner against subprocess orchestration and signal handling test suites to confirm graceful termination.
npm test -- subprocess || yarn test subprocess
```

**Accept when:**
- Subprocess executions use execa and register SIGINT signal listeners that terminate active child process handles.
- Interruption during execution results in all child processes being terminated without orphaned background tasks.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by static code analysis scanning for execa usage and associated SIGINT signal handler registrations, automated test suites verifying process termination behavior during interruption signals, and peer code review for changes introducing external process execution. Violation handling: Pull requests lacking required signal cleanup for spawned processes are blocked until lifecycle handlers are implemented, and automated linting failures flagging unhandled child process executions must be resolved before merging.
</enforcement>