---
version: 2
name: cross-cutting-benchmark-suites-not-invoke-unabstracted-8fc7
description: "Adoption of execa for Subprocess Execution in Benchmark Suites: Benchmark Suites Not Invoke Unabstracted Core"
metadata:
  actual:
    adr_id: 8fc7fea4-4d35-40b3-95a0-b7806b256c45
    status: accepted
    candidate_group_id: 732ee91a-e074-4c4e-bb43-f12941fb2992
    evidence:
      source: deep
  scope:
    root: packages/tsc
    paths:
      - bench/**
---

# Adoption of execa for Subprocess Execution in Benchmark Suites: Benchmark Suites Not Invoke Unabstracted Core

Scope: applies to `packages/tsc/bench/**`.

These rules are ALWAYS ACTIVE for benchmark harness suites and performance measurement suites executing external processes.

### Rules

- **R-EXEC-001** MUST_NOT: Benchmark suites MUST NOT invoke unabstracted core runtime child process spawning APIs directly when execa is available as the adopted process execution interface.
- **R-EXEC-002** MANDATORY: The consumer MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository following the discovery policy.
- **R-EXEC-003** MANDATORY: Before writing code that uses a versioned library, execute in order: find dependency manifest, identify build tool, inspect repository lock or resolution artifact for the exact resolved version, look up official documentation for that exact version, and confirm every API/class/function exists.
- **R-EXEC-004** MANDATORY: Benchmark suites should encapsulate shared fixture generation and parameter setup in reusable helper modules before invoking execa for compiler execution.
- **R-EXEC-005** MANDATORY: Process outputs should be inspected for error exit codes and process signal terminations to ensure benchmark metrics only record successful executions.

### Verify

```bash
# Discover the benchmark execution task in the project task configuration and run the benchmark suite to verify child process execution.
# Inspect repository dependency declarations to confirm execa is declared within the appropriate workspace dependency scope.
```

**Accept when:**
- All benchmark execution suites spawn external processes through execa without runtime failures.
- Automated benchmark runs complete with deterministic exit codes and clean child process termination.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>