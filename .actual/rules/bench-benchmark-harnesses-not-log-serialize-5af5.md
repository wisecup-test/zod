# Direct Process Environment Access via process.env for Benchmark Configuration: Benchmark Harnesses Not Log Serialize Dump

These rules are ALWAYS ACTIVE for performance benchmarking harnesses and test suites requiring runtime execution toggles or filter configurations.

### Rules

- **R-BENCH-001** MUST_NOT: Benchmark harnesses MUST_NOT log, serialize, or dump raw ambient environment dictionaries or unredacted execution contexts to console outputs, benchmark summary tables, or artifact stores.

### Verify

```bash
# Discover and run the repository static analysis and security scanning script from the root manifest
# Locate and execute the benchmark test execution script defined in the project manifest
```

**Accept when:**
- Static analysis checks pass without flagging unauthorized ambient environment variable reads or unredacted credential exposures.
- Benchmark execution completes successfully using defined configuration defaults when ambient environment variables are unset.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>