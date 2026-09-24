# benchmark Event-Driven Lifecycle Integration: Consumers Inspect Repository Lock Artifact Verify

These rules are ALWAYS ACTIVE for performance benchmarking suites and execution harnesses within the project.

### Rules

- **R-BENCH-001** MUST: Consumers MUST inspect the repository lock artifact to verify the exact resolved version of the benchmark library prior to implementing or modifying benchmark suites.

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