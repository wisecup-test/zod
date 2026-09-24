# Process Environment Variable Configuration for Benchmark Execution: Benchmark Execution Modules Restrict Direct Process

These rules are ALWAYS ACTIVE for runtime configuration for benchmark suites and performance measurement modules.

### Rules

- **R-BENCH-001** MUST: Benchmark execution modules MUST restrict direct process environment variable reads to operational toggles and execution flags specific to benchmark execution.

### Verify

```bash
# Discover and execute the repository benchmark verification script defined in the project configuration.
# Discover and execute the repository static analysis and type checking verification scripts.
```

**Accept when:**
- Benchmark suites execute cleanly with and without environment variable overrides.
- Static analysis verification confirms no unhandled or undeclared environment variables in benchmark modules.
- Benchmark execution outputs show performance metrics without leaking ambient environment state.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>