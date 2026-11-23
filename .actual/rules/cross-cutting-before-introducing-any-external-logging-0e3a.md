---
version: 2
name: cross-cutting-before-introducing-any-external-logging-0e3a
description: "Console Logging API for Command-Line Diagnostics: Before Introducing Any External Logging Dependency"
metadata:
  actual:
    adr_id: 0e3a7737-5e69-46de-a69d-624ac8466d48
    status: accepted
    candidate_group_id: 5ac8fa6c-ba70-4a06-a6bf-6c44c9428bc0
    evidence:
      source: deep
  scope:
    root: packages/tsc
    paths:
      - bench/**
---

# Console Logging API for Command-Line Diagnostics: Before Introducing Any External Logging Dependency

Scope: applies to `packages/tsc/bench/**`.

These rules are ALWAYS ACTIVE for:
- Command-line execution scripts and benchmarking harnesses requiring interactive terminal output.

### Rules

- **R-L-001** MUST: Before introducing any external logging dependency or versioned utility, the consumer MUST inspect the repository lock artifact to verify the exact resolved version and adhere to its published API specification.

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
