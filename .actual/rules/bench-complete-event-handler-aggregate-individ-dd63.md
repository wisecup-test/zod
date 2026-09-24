# benchmark Event-Driven Lifecycle Integration: Complete Event Handler Aggregate Individual Benchmark

These rules are ALWAYS ACTIVE for all performance benchmarking suites and execution harnesses within the project.

### Rules

- **R-BENCH-001** MUST: The complete event handler MUST aggregate individual benchmark metrics including operations per second, mean execution duration, and relative margin of error into structured comparative outputs.

### Verify

```bash
# Discover and run the project benchmark suite script defined in the repository configuration
# Inspect benchmark execution output to confirm cycle progress and completion tables render without errors
```

**Accept when:**
- Benchmark suite runs to completion and emits cycle notifications followed by a tabular summary.
- Reported metrics contain throughput, mean duration, and error margin calculations.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>