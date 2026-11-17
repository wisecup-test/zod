---
version: 2
name: cross-cutting-child-process-tracking-collections-remov-56dd
description: "Execa Subprocess Execution with SIGINT Interruption Lifecycle Cleanup: Child Process Tracking Collections Remove Terminated"
metadata:
  actual:
    adr_id: 56dd57da-9c92-4605-8295-b72c16e9f37a
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

# Execa Subprocess Execution with SIGINT Interruption Lifecycle Cleanup: Child Process Tracking Collections Remove Terminated

Scope: applies to `packages/tsc/bench/**`, `packages/tsc/bisect.ts`.

These rules are ALWAYS ACTIVE for modules and scripts that orchestrate asynchronous external subprocess executions, as well as CLI task runners and benchmarking harnesses managing long-running child processes.

### Rules

- **R-EXEC-001** SHOULD: Child process tracking collections SHOULD remove terminated or exited child process references dynamically to minimize memory retention during extended executions.
- **R-EXEC-002** MANDATORY: Maintain a collection of running child process instances returned by execa and register a process.on listener for SIGINT to iterate and kill remaining active processes.
- **R-EXEC-003** MANDATORY: Check the killed property on child process objects before issuing kill calls to avoid redundant termination signals on already-exited processes.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify compliance with process execution and signal handler conventions.
# Discover and execute the project test runner against subprocess orchestration and signal handling test suites to confirm graceful termination.
```

**Accept when:**
- Subprocess executions use execa and register SIGINT signal listeners that terminate active child process handles.
- Interruption during execution results in all child processes being terminated without orphaned background tasks.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by static code analysis scanning for execa usage and associated SIGINT signal handler registrations, automated test suites verifying process termination behavior during interruption signals, and peer code review for changes introducing external process execution.
</enforcement>