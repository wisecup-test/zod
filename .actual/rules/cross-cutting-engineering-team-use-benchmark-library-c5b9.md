# Adoption of benchmark Library for Performance Benchmarking Suites: Engineering Team Use Benchmark Library Standardized

These rules are ALWAYS ACTIVE for all performance benchmarking suites, schema validation, parsing operations, and comparative runtime throughput evaluations across packages.

### Rules

- **R-BENCH-001** MUST: Use the benchmark library as the standardized framework for defining and executing performance benchmark suites across validation and runtime modules.
- **R-BENCH-002** MANDATORY: Discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-BENCH-003** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: (1) Find dependency manifest, (2) Identify build tool, (3) Inspect repository lock/resolution artifact, (4) Look up official docs for that exact version, (5) Confirm every API/class/function exists in that version, (6) Re-run steps 3-5 per dependency at point of use.
- **R-BENCH-004** MUST: Keep benchmark cases stateless and idempotent to allow thousands of consecutive iterations without memory accumulation or side-effect leakage.
- **R-BENCH-005** MUST: Enforce local error trapping within benchmark callbacks for invalid input scenarios to prevent unhandled exceptions from aborting the suite prematurely.

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
Claude Code MUST NOT skip or defer verification. Continuous integration benchmark performance validation jobs and peer code reviews enforce compliance, and pull requests containing unhandled benchmark exceptions or non-standard benchmark runners are blocked from merging.
</enforcement>