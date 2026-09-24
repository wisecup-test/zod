# execa Process Execution Library Adoption: Spawning Invocations Capture Standard Output Error

These rules are ALWAYS ACTIVE for benchmarking suites, bisection tools, and resolution verification scripts that spawn external commands or helper modules, as well as utility scripts that manage concurrent or sequential child process execution lifecycles.

### Rules

- **R-EX-001** SHOULD: Spawning invocations SHOULD capture standard output and standard error streams asynchronously using the promise-based interfaces provided by execa.

### Verify

```bash
# Discover and run the project's static analysis and dependency verification scripts to confirm execa import compliance.
# Discover and run the project's automated test suite to ensure benchmarking and verification scripts execute and terminate child processes cleanly.
```

**Accept when:**
- All subprocess invocations within tooling and benchmark modules import and use execa.
- Process execution scripts register interruption handlers that successfully terminate active child processes upon signal dispatch.
- Project verification suites pass without unhandled child process rejections or zombie processes.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated linting, continuous integration test runs validating benchmark execution and clean process termination, and peer review for all modifications to child process invocation logic.
</enforcement>