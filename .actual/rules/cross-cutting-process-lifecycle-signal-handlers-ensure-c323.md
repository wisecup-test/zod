---
version: 2
name: cross-cutting-process-lifecycle-signal-handlers-ensure-c323
description: "Console Logging API for Command-Line Diagnostics: Process Lifecycle Signal Handlers Ensure Termination"
metadata:
  actual:
    adr_id: c323bc35-6476-4575-98de-a35b1258e254
    status: accepted
    candidate_group_id: 5ac8fa6c-ba70-4a06-a6bf-6c44c9428bc0
    evidence:
      source: deep
  scope:
    root: packages/tsc
    paths:
      - bench/**
---

# Console Logging API for Command-Line Diagnostics: Process Lifecycle Signal Handlers Ensure Termination

Scope: applies to `packages/tsc/bench/**`.

These rules are ALWAYS ACTIVE for command-line execution scripts and benchmarking harnesses requiring interactive terminal output.

### Rules

- **R-CLI-001** MUST: Process lifecycle signal handlers MUST ensure termination status messages are written to the standard output stream prior to triggering process exit.

### Verify

```bash
# Discover and run the project static analysis and linting verification scripts to check logging conventions across script boundaries.
# Discover and execute the repository test suite to ensure benchmarking scripts exit with expected status codes on invalid arguments.
```

**Accept when:**
- Static analysis validates that console output invocations are restricted to designated utility and script directories.
- Executing the benchmark script with missing arguments outputs an actionable error message to standard error and halts execution.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via static analysis and automated checks.
</enforcement>