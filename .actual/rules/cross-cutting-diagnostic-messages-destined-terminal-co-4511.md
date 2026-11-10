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

These rules are ALWAYS ACTIVE for command-line execution scripts and benchmarking harnesses requiring interactive terminal output.

### Rules

- **R-DIAG-001** SHOULD: Diagnostic messages destined for terminal consumers SHOULD separate error notifications on standard error from standard runtime process output.

### Verify

```bash
# Discover and run the project static analysis and linting verification scripts to check logging conventions across script boundaries.
# Discover and execute the repository test suite to ensure benchmarking scripts exit with expected status codes on invalid arguments.
```

**Accept when:**
- Static analysis validates that console output invocations are restricted to designated utility and script directories.
- Executing the benchmark script with missing arguments outputs an actionable error message to standard error and halts execution.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated static analysis checks in continuous integration pipelines and peer review during pull requests.
</enforcement>