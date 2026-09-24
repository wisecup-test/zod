# Direct Process Environment Access via process.env for Benchmark Configuration: Non Secret Benchmark Control Flags Clearly

These rules are ALWAYS ACTIVE for performance benchmarking harnesses and test suites requiring runtime execution toggles or filter configurations.

### Rules

- **R-BENCH-001** SHOULD: Non-secret benchmark control flags SHOULD be clearly separated from sensitive credentials and system secret stores through dedicated configuration namespaces.

### Verify

```bash
# Discover the repository static analysis and security scanning script from the root manifest and run it to verify no sensitive credentials or direct ambient environment variables are leaked in benchmark reporting.
# Locate the benchmark test execution script defined in the project manifest and execute the test runner to validate configuration schema handling.
```

**Accept when:**
- Static analysis checks pass without flagging unauthorized ambient environment variable reads or unredacted credential exposures.
- Benchmark execution completes successfully using defined configuration defaults when ambient environment variables are unset.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated static analysis checks in the continuous integration pipeline scanning for raw process.env access and peer code review.
</enforcement>