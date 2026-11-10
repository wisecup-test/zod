---
version: 2
name: cross-cutting-event-listener-callbacks-registered-benc-8032
description: "Benchmark Suite Event-Driven Lifecycle Integration: Event Listener Callbacks Registered Benchmark Suites"
metadata:
  actual:
    adr_id: 8032a796-b672-46a8-8266-29a32398b0f8
    status: accepted
    candidate_group_id: 58e9da9d-b094-48a3-acf6-7db168163a94
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v3/benchmarks/**
---

# Benchmark Suite Event-Driven Lifecycle Integration: Event Listener Callbacks Registered Benchmark Suites

Scope: applies to `packages/zod/src/v3/benchmarks/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ADR-001** MUST: Event listener callbacks registered on benchmark suites MUST accept the benchmark event object and read execution targets directly from the event target property.

### Verify

```bash
# Discover the repository benchmark script defined in the dependency manifest and execute it to verify suite cycle output.
# Inspect benchmark suite definitions to ensure test lambdas do not contain standard input and output or logging statements.
```

**Accept when:**
- Benchmark suites execute and emit cycle events reporting target completion without throwing unhandled exceptions.
- All benchmark suites register cycle event listeners via the on method and exclude logging logic from add test lambdas.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>