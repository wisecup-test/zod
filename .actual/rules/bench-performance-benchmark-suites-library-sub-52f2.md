# benchmark Event-Driven Lifecycle Integration: Performance Benchmark Suites Library Subscribe Lifecycle

These rules are ALWAYS ACTIVE for all performance benchmarking suites and execution harnesses within the project.

### Rules

- **R-BENCH-001** MUST: Performance benchmark suites using the benchmark library MUST subscribe to lifecycle events including cycle and complete to coordinate execution progress and result aggregation.

### Verify

```bash
# Discover and run the project benchmark suite script defined in the repository configuration.
# Inspect benchmark execution output to confirm cycle progress and completion tables render without errors.
```

**Accept when:**
- Benchmark suite runs to completion and emits cycle notifications followed by a tabular summary.
- Reported metrics contain throughput, mean duration, and error margin calculations.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>