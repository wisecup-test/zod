# Direct Process Environment Access via process.env for Benchmark Configuration: Benchmark Suites Isolate Runtime Configuration Ingestion

These rules are ALWAYS ACTIVE for performance benchmarking harnesses and test suites requiring runtime execution toggles or filter configurations.

### Rules

- **R-BENCH-001** MUST: Benchmark suites MUST isolate runtime configuration ingestion by defining explicit, typed configuration schemas rather than reading unvalidated global process.env properties directly across benchmark execution files.

### Verify

```bash
# Discover and run the project's static analysis or security scanning script to verify no direct ambient environment variables are leaked
# Locate and execute the benchmark test runner defined in the project manifest to validate configuration schema handling
```

**Accept when:**
- Static analysis checks pass without flagging unauthorized ambient environment variable reads or unredacted credential exposures.
- Benchmark execution completes successfully using defined configuration defaults when ambient environment variables are unset.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis and peer code review enforce compliance, and CI builds fail upon detection of raw ambient environment reads outside sanctioned configuration boundary modules.
</enforcement>