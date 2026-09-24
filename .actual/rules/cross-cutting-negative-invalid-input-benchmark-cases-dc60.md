# Adoption of benchmark Library for Performance Benchmarking Suites: Negative Invalid Input Benchmark Cases Encapsulate

These rules are ALWAYS ACTIVE for performance benchmarking suites, negative invalid input benchmark cases, and schema validation/parsing latency regression testing across packages.

### Rules

- **R-BENCH-001** MUST: Negative and invalid input benchmark cases MUST encapsulate expected parsing failures within local exception handling blocks to prevent premature suite termination.

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