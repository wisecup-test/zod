---
version: 2
name: cross-cutting-child-processes-managed-execa-enforce-b343
description: "Adoption of execa for Subprocess Execution in Benchmark Suites: Child Processes Managed Execa Enforce Deterministic"
metadata:
  actual:
    adr_id: b3437733-acdb-45db-8bb5-f847d3655631
    status: accepted
    candidate_group_id: 732ee91a-e074-4c4e-bb43-f12941fb2992
    evidence:
      source: deep
  scope:
    root: packages/tsc
    paths:
      - bench/**
---

# Adoption of execa for Subprocess Execution in Benchmark Suites: Child Processes Managed Execa Enforce Deterministic

Scope: applies to `packages/tsc/bench/**`.

These rules are ALWAYS ACTIVE for benchmark harness suites and performance measurement suites executing external processes, and integration benchmarks requiring programmatic compiler process invocation.

### Rules

- **R-EXEC-001** MUST: Child processes managed by execa MUST enforce deterministic execution timeout limits to prevent hung processes from blocking automated benchmarking pipelines.

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