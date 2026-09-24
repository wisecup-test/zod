# Adoption of benchmark Library for Performance Benchmarking Suites: Consumers Inspect Repository Lock Resolution Artifact

These rules are ALWAYS ACTIVE for performance benchmarking suites, comparative runtime throughput evaluations, schema parsing latency, date validation, and object structure processing.

### Rules

- **R-BENCH-001** MUST: Consumers MUST inspect the repository lock or resolution artifact to determine and adhere to the exact resolved version of the benchmark library prior to implementation.
- **R-BENCH-002** MUST: Execute lock-version grounding in order: find dependency manifest, identify build tool, inspect repository lock or resolution artifact for exact resolved version, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run steps per dependency at point of use.
- **R-BENCH-003** MUST: Benchmark cases must remain stateless and idempotent to allow thousands of consecutive iterations without memory accumulation or side-effect leakage.
- **R-BENCH-004** MUST: Enforce local error trapping within benchmark callbacks for invalid input scenarios to prevent uncaught exceptions from aborting the benchmark suite prematurely.

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