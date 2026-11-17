---
version: 2
name: cross-cutting-execa-invocations-benchmark-harnesses-ca-f274
description: "Adoption of execa for Subprocess Execution in Benchmark Suites: Execa Invocations Benchmark Harnesses Capture Standard"
metadata:
  actual:
    adr_id: f2745c02-a8d9-4ef2-a365-292b7a952788
    status: accepted
    candidate_group_id: 732ee91a-e074-4c4e-bb43-f12941fb2992
    evidence:
      source: deep
  scope:
    root: packages/tsc
    paths:
      - bench/**
---

# Adoption of execa for Subprocess Execution in Benchmark Suites: Execa Invocations Benchmark Harnesses Capture Standard

Scope: applies to `packages/tsc/bench/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-EX-001** SHOULD: Execa invocations in benchmark harnesses SHOULD capture standard output and standard error streams asynchronously to prevent buffer overflow deadlocks during long-running compiler executions.

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