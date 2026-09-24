# Adoption of benchmark Library for Performance Benchmarking Suites: Performance Suites Register Event Listeners Cycle

These rules are ALWAYS ACTIVE for all performance benchmarking suites and comparative runtime throughput evaluations across packages.

### Rules

- **R-PERF-001** MUST: Performance suites MUST register event listeners for cycle completion events to observe incremental benchmark progress and target statistics.

### Verify

```bash
# Discover the project configuration manifest and execute the designated benchmark runner script to verify suite compilation and execution.
# Inspect benchmark execution output to confirm that cycle event reporting and completion summary metrics emit valid statistical samples without uncaught exceptions.
```

**Accept when:**
- The benchmark execution script runs to completion across all defined suites without runtime failures.
- Benchmark cycle listeners emit per-target operations per second and sample counts for each benchmark case.
- Completion handlers output relative margin of error and comparative performance rankings.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>