# execa Process Execution Library Adoption: Modules Within Scope Not Execute Child

These rules are ALWAYS ACTIVE for benchmarking suites, bisection tools, resolution verification scripts, and utility scripts that manage concurrent or sequential child process execution lifecycles.

### Rules

- **R-EXEC-001** MUST_NOT: Modules within scope MUST_NOT execute child processes using unmanaged shell strings or untracked background processes that bypass interruption signal cleanup.
- **R-EXEC-002** MUST: Maintain an internal registry or collection of active child process references within long-running automation scripts so that signal handlers can iterate and terminate outstanding processes.
- **R-EXEC-003** MUST: Handle standard stream outputs using asynchronous promise interfaces to capture errors and output without blocking runtime execution.
- **R-EXEC-004** MUST: Adhere to the lock-version grounding policy by verifying resolved lock artifact versions and public API documentation before adopting new method signatures.

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
Claude Code MUST NOT skip or defer verification. All subprocess invocations within tooling and benchmark modules must import and use execa, register interruption handlers for process cleanup, and pass project verification suites without unhandled child process rejections or zombie processes.
</enforcement>