---
version: 2
name: cross-cutting-before-integrating-updating-process-exec-b488
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

Scope: applies to `packages/tsc/bench/**`, `packages/tsc/bisect.ts`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-PROC-001** MUST: Before integrating or updating the process execution dependency, developers MUST inspect the repository dependency manifest and lock artifact to verify the exact resolved dependency version and its documented process lifecycle APIs.
- **R-PROC-002** MUST: Maintain a collection of running child process instances and register a process.on listener for SIGINT to iterate and kill remaining active processes.
- **R-PROC-003** MUST: Check the killed property on child process objects before issuing kill calls to avoid redundant termination signals on already-exited processes.
- **R-PROC-004** MUST: Attach completion listeners to child processes to prune completed handles from the active process tracking collection.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify compliance with process execution and signal handler conventions.
# Discover and execute the project test runner against subprocess orchestration and signal handling test suites to confirm graceful termination.
```

**Accept when:**
- Subprocess executions use execa and register SIGINT signal listeners that terminate active child process handles.
- Interruption during execution results in all child processes being terminated without orphaned background tasks.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>