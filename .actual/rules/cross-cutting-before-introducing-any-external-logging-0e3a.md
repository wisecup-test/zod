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

These rules are ALWAYS ACTIVE for command-line execution scripts and benchmarking harnesses requiring interactive terminal output.

### Rules

- **R-LOG-001** MUST: Before introducing any external logging dependency or versioned utility, the consumer MUST inspect the repository lock artifact to verify the exact resolved version and adhere to its published API specification.

### Verify

```bash
# Discover and run the project static analysis and linting verification scripts to check logging conventions across script boundaries.
# Discover and execute the repository test suite to ensure benchmarking scripts exit with expected status codes on invalid arguments.
```

**Accept when:**
- Static analysis validates that console output invocations are restricted to designated utility and script directories.
- Executing the benchmark script with missing arguments outputs an actionable error message to standard error and halts execution.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis and peer reviews enforce that console output invocations are restricted to designated directories and dependencies are strictly verified against lock artifacts.
</enforcement>