# execa Process Execution Library Adoption: Automated Benchmark Scripts Bisection Utilities Resolution

These rules are ALWAYS ACTIVE for automated benchmark scripts, bisection utilities, resolution test suites, and related diagnostic modules requiring programmatic execution of external processes and script targets.

### Rules

- **R-EXEC-001** MUST: All automated benchmark scripts, bisection utilities, and resolution test suites requiring child process execution MUST use execa as the standardized process spawning library.
- **R-EXEC-002** MANDATORY: Execute the discovery policy and lock-version grounding sequence before writing code that uses a versioned library: (1) Find the dependency manifest, (2) Identify the build tool, (3) Inspect the repository lock or resolution artifact for the exact resolved version, (4) Look up official documentation/changelog for that exact version, (5) Confirm every API/class/function exists in that version, (6) Re-run steps 3-5 per dependency at point of use.
- **R-EXEC-003** MUST: Maintain an internal registry or collection of active child process references within long-running automation scripts so that signal handlers can iterate and terminate outstanding processes.
- **R-EXEC-004** MUST: Handle standard stream outputs using asynchronous promise interfaces to capture errors and output without blocking runtime execution.

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
Claude Code MUST NOT skip or defer verification. All modifications to child process invocation logic are verified by automated linting, CI test runs, and peer review. Violations will block pull requests until refactored.
</enforcement>