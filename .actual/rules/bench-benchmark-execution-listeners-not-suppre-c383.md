# benchmark Event-Driven Lifecycle Integration: Benchmark Execution Listeners Not Suppress Discard

These rules are ALWAYS ACTIVE for performance benchmarking suites and execution harnesses within the project.

### Rules

- **R-BED-001** MUST_NOT: Benchmark execution listeners MUST NOT suppress or discard cycle completion events during suite execution.

### Verify

```bash
# Discover and run the project benchmark suite script defined in the repository configuration
# Inspect benchmark execution output to confirm cycle progress and completion tables render without errors
```

**Accept when:**
- Benchmark suite runs to completion and emits cycle notifications followed by a tabular summary.
- Reported metrics contain throughput, mean duration, and error margin calculations.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification by automated continuous integration and peer code review is mandatory.
</enforcement>