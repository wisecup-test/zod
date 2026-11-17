---
version: 2
name: cross-cutting-command-line-benchmarking-scripts-use-ea3d
description: "Console Logging API for Command-Line Diagnostics: Command Line Benchmarking Scripts Use Runtime"
metadata:
  actual:
    adr_id: ea3dc18a-accc-4843-abd1-5544b2aa9017
    status: accepted
    candidate_group_id: 5ac8fa6c-ba70-4a06-a6bf-6c44c9428bc0
    evidence:
      source: deep
  scope:
    root: packages/tsc
    paths:
      - bench/**
---

# Console Logging API for Command-Line Diagnostics: Command Line Benchmarking Scripts Use Runtime

Scope: applies to `packages/tsc/bench/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CLI-001** MUST: Command-line benchmarking scripts MUST use the runtime console error interface to emit usage guidance and validation failure messages to the standard error stream.

### Verify

```bash
# Discover and run the project static analysis and linting verification scripts to check logging conventions across script boundaries.
# Discover and execute the repository test suite to ensure benchmarking scripts exit with expected status codes on invalid arguments.
```

**Accept when:**
- Static analysis validates that console output invocations are restricted to designated utility and script directories.
- Executing the benchmark script with missing arguments outputs an actionable error message to standard error and halts execution.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>