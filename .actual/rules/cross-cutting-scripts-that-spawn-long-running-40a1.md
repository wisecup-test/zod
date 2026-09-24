# execa Process Execution Library Adoption: Scripts That Spawn Long Running Iterative

These rules are ALWAYS ACTIVE for benchmarking suites, bisection tools, resolution verification scripts, and utility scripts that manage concurrent or sequential child process execution lifecycles.

### Rules

- **R-EXA-001** MUST: Scripts that spawn long-running, iterative, or concurrent child processes MUST register interruption signal handlers to terminate active child processes before exiting the parent process.

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
Claude Code MUST NOT skip or defer verification. All subprocess invocations and process execution scripts must be verified via static analysis, test execution, and peer review.
</enforcement>