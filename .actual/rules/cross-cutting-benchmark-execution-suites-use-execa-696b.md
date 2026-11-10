---
version: 2
name: cross-cutting-benchmark-execution-suites-use-execa-696b
description: "Adoption of execa for Subprocess Execution in Benchmark Suites: Benchmark Execution Suites Use Execa Spawning"
metadata:
  actual:
    adr_id: 696bec8e-0d23-41a8-b393-a5e40eef1e42
    status: accepted
    candidate_group_id: 732ee91a-e074-4c4e-bb43-f12941fb2992
    evidence:
      source: deep
  scope:
    root: packages/tsc
    paths:
      - bench/**
---

# Adoption of execa for Subprocess Execution in Benchmark Suites: Benchmark Execution Suites Use Execa Spawning

Scope: applies to `packages/tsc/bench/**`.

These rules are ALWAYS ACTIVE for benchmark harness suites, performance measurement suites executing external processes, and integration benchmarks requiring programmatic compiler process invocation.

### Rules

- **R-EXEC-001** MUST: Benchmark execution suites MUST use execa for spawning, monitoring, and terminating external child processes during performance benchmarking runs.

### Verify

```bash
# Discover the benchmark execution task in the project task configuration and run the benchmark suite
# Inspect repository dependency declarations to confirm execa is declared within the appropriate workspace dependency scope
```

**Accept when:**
- All benchmark execution suites spawn external processes through execa without runtime failures.
- Automated benchmark runs complete with deterministic exit codes and clean child process termination.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipeline execution and static code review verify process invocation compliance.
</enforcement>