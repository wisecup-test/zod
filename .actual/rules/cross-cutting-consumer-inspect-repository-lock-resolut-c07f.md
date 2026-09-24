# execa Process Execution Library Adoption: Consumer Inspect Repository Lock Resolution Artifact

These rules are ALWAYS ACTIVE for benchmarking suites, bisection tools, resolution verification scripts, and utility scripts that manage concurrent or sequential child process execution lifecycles.

### Rules

- **R-EXEC-001** MUST: The consumer MUST inspect the repository lock or resolution artifact to determine the exact resolved version of execa prior to implementation, verifying that all invoked APIs conform to that exact version reference.

### Verify

```bash
# Discover and run the project's static analysis and dependency verification scripts to confirm execa import compliance
# Discover and run the project's automated test suite to ensure benchmarking and verification scripts execute and terminate child processes cleanly
```

**Accept when:**
- All subprocess invocations within tooling and benchmark modules import and use execa.
- Process execution scripts register interruption handlers that successfully terminate active child processes upon signal dispatch.
- Project verification suites pass without unhandled child process rejections or zombie processes.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated linting, static analysis checks, CI pipeline test runs, and peer review.
</enforcement>