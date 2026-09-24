# Direct Process Environment Access via process.env for Benchmark Configuration: Before Consuming Any External Configuration Validation

These rules are ALWAYS ACTIVE for performance benchmarking harnesses and test suites requiring runtime execution toggles or filter configurations.

### Rules

- **R-ENV-001** MUST: Before consuming any external configuration or validation dependencies, developers MUST discover the authoritative repository lock artifact and verify the exact resolved dependency versions.
- **R-ENV-002** MUST: Encapsulate benchmark configuration parsing in a dedicated setup module that sanitizes input parameters before instantiating benchmark suites.
- **R-ENV-003** MUST: Verify that benchmark reporting formatters only include benchmark timing statistics and exclude raw runtime configuration objects from final tabular outputs.

### Verify

```bash
# Discover the repository static analysis and security scanning script from the root manifest and run it to verify no sensitive credentials or direct ambient environment variables are leaked in benchmark reporting.
# Locate the benchmark test execution script defined in the project manifest and execute the test runner to validate configuration schema handling.
```

**Accept when:**
- Static analysis checks pass without flagging unauthorized ambient environment variable reads or unredacted credential exposures.
- Benchmark execution completes successfully using defined configuration defaults when ambient environment variables are unset.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>