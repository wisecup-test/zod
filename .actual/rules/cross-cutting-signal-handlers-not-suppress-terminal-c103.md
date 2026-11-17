---
version: 2
name: cross-cutting-signal-handlers-not-suppress-terminal-c103
description: "Execa Subprocess Execution with SIGINT Interruption Lifecycle Cleanup: Signal Handlers Not Suppress Terminal Errors"
metadata:
  actual:
    adr_id: c103132e-1b7b-4eb3-ad09-2c01d6f95c84
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

# Execa Subprocess Execution with SIGINT Interruption Lifecycle Cleanup: Signal Handlers Not Suppress Terminal Errors

Scope: applies to `packages/tsc/bench/**`, `packages/tsc/bisect.ts`.

These rules are ALWAYS ACTIVE for modules and scripts that orchestrate asynchronous external subprocess executions and CLI task runners and benchmarking harnesses managing long-running child processes.

### Rules

- **R-EXEC-001** MUST_NOT: Signal handlers MUST_NOT suppress terminal errors silently without terminating tracked child process handles.

### Verify

```bash
# Discover and run the project static analysis, linting, and test suites
# (Commands to be discovered from the project repository configuration)
```

**Accept when:**
- Subprocess executions use execa and register SIGINT signal listeners that terminate active child process handles.
- Interruption during execution results in all child processes being terminated without orphaned background tasks.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>