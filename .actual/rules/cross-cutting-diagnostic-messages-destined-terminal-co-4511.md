---
version: 2
name: cross-cutting-diagnostic-messages-destined-terminal-co-4511
description: "Console Logging API for Command-Line Diagnostics: Diagnostic Messages Destined Terminal Consumers Separate"
metadata:
  actual:
    adr_id: 45112b4a-f1e8-4c30-b886-c66c9c5825ae
    status: accepted
    candidate_group_id: 5ac8fa6c-ba70-4a06-a6bf-6c44c9428bc0
    evidence:
      source: deep
  scope:
    root: packages/tsc
    paths:
      - bench/**
---

# Console Logging API for Command-Line Diagnostics: Diagnostic Messages Destined Terminal Consumers Separate

Scope: applies to `packages/tsc/bench/**`.

These rules are ALWAYS ACTIVE for:
- Command-line execution scripts and benchmarking harnesses requiring interactive terminal output.

### Rules

- **R-L-001** SHOULD: Diagnostic messages destined for terminal consumers SHOULD separate error notifications on standard error from standard runtime process output.

### Verify

- Discover and run the project static analysis and linting verification scripts to check logging conventions across script boundaries.
- Discover and execute the repository test suite to ensure benchmarking scripts exit with expected status codes on invalid arguments.

**Accept when:**

- Static analysis validates that console output invocations are restricted to designated utility and script directories.
- Executing the benchmark script with missing arguments outputs an actionable error message to standard error and halts execution.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated static analysis checks in continuous integration pipelines.
- Verified by: Peer review during pull requests affecting utility and benchmarking scripts.
- Violation handling: Pull requests containing unauthorized direct console invocations outside permitted script directories are blocked until resolved.
- Exception process: Exceptions for temporary debugging logs or alternative logging utilities must be documented in code comments and approved by module maintainers.
</enforcement>
