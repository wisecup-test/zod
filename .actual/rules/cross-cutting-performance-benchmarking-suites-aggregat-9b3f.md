# Adoption of benchmark Library for Performance Benchmarking Suites: Performance Benchmarking Suites Aggregate Sample Metrics

These rules are ALWAYS ACTIVE for performance benchmarking suites, comparative runtime throughput evaluations, schema parsing latency, date validation, and object structure processing.

### Rules

- **R-BENCH-001** SHOULD: Performance benchmarking suites aggregate sample metrics, mean execution times, operations per second, and relative margin of error upon suite completion to evaluate comparative performance.
- **R-BENCH-002** MANDATORY (DISCOVERY POLICY): Omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.
- **R-BENCH-003** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: (1) Find the dependency manifest in the repo. (2) Identify the build tool from the manifest. (3) Inspect the repository lock or resolution artifact to determine the exact resolved version. (4) Look up official documentation/changelog/public API reference for that exact version without relying solely on training data. (5) Confirm every API, class, or function used exists in that exact version's documentation. (6) Re-run steps 3-5 per dependency at point of use for version-sensitive behavior.
- **R-BENCH-004** MANDATORY: Benchmark cases must remain stateless and idempotent to allow thousands of consecutive iterations without memory accumulation or side-effect leakage.
- **R-BENCH-005** MANDATORY: Suite completion handlers should sort and tabulate operations per second alongside relative speedup multiples to clearly convey comparative throughput.

### Verify

```bash
# Discover the project configuration manifest and execute the designated benchmark runner script
# to verify suite compilation and execution, and inspect output to confirm valid statistical samples.
# (Commands must be derived from the project repository configuration files)
```

**Accept when:**
- The benchmark execution script runs to completion across all defined suites without runtime failures.
- Benchmark cycle listeners emit per-target operations per second and sample counts for each benchmark case.
- Completion handlers output relative margin of error and comparative performance rankings.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>