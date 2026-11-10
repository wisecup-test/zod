---
version: 2
name: cross-cutting-any-execution-routine-that-spawns-920b
description: "Execa Subprocess Execution with SIGINT Interruption Lifecycle Cleanup: Any Execution Routine That Spawns Child"
metadata:
  actual:
    adr_id: 920b9c2b-72d8-45e0-95df-5176a3803215
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

# Execa Subprocess Execution with SIGINT Interruption Lifecycle Cleanup: Any Execution Routine That Spawns Child

Scope: applies to `packages/tsc/bench/**`, `packages/tsc/bisect.ts`.

These rules are ALWAYS ACTIVE for modules and scripts that orchestrate asynchronous external subprocess executions, CLI task runners, and benchmarking harnesses managing long-running child processes.

### Rules

- **R-EXEC-001** MUST: Any execution routine that spawns child processes MUST track active child process handles and verify the process killed property before initiating termination.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify compliance with process execution and signal handler conventions.
npm run lint || pnpm run lint || yarn lint

# Discover and execute the project test runner against subprocess orchestration and signal handling test suites to confirm graceful termination.
npm test || pnpm test || yarn test
```

**Accept when:**
- Subprocess executions use execa and register SIGINT signal listeners that terminate active child process handles.
- Interruption during execution results in all child processes being terminated without orphaned background tasks.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>