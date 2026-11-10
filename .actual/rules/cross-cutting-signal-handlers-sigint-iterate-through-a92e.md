---
version: 2
name: cross-cutting-signal-handlers-sigint-iterate-through-a92e
description: "Execa Subprocess Execution with SIGINT Interruption Lifecycle Cleanup: Signal Handlers Sigint Iterate Through Tracked"
metadata:
  actual:
    adr_id: a92e02ff-f8af-402c-b445-e5c9ffc6c313
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

# Execa Subprocess Execution with SIGINT Interruption Lifecycle Cleanup: Signal Handlers Sigint Iterate Through Tracked

Scope: applies to `packages/tsc/bench/**`, `packages/tsc/bisect.ts`.

These rules are ALWAYS ACTIVE for modules and scripts that orchestrate asynchronous external subprocess executions, CLI task runners, and benchmarking harnesses managing long-running child processes.

### Rules

- **R-EXEC-001** MUST: Signal handlers for SIGINT MUST iterate through all tracked active child process instances and invoke their kill method to prevent orphaned background processes.

### Verify

```bash
# Discover and run the project static analysis and linting scripts
# Discover and execute the project test runner against subprocess orchestration and signal handling test suites
```

**Accept when:**
- Subprocess executions use execa and register SIGINT signal listeners that terminate active child process handles.
- Interruption during execution results in all child processes being terminated without orphaned background tasks.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>