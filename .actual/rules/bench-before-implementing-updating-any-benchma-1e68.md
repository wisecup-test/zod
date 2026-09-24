# Process Environment Variable Configuration for Benchmark Execution: Before Implementing Updating Any Benchmark Execution

These rules are ALWAYS ACTIVE for runtime configuration for benchmark suites and performance measurement modules.

### Rules

- **R-BENCH-001** MUST: Before implementing or updating any benchmark execution dependency, the consumer MUST inspect the repository dependency lock artifact to determine and verify the exact resolved version.
- **R-BENCH-002** MUST: Locate benchmark suites within the repository and verify that process environment access is confined to benchmark execution toggles.
- **R-BENCH-003** MUST: Ensure that benchmark reporting formatting utilities only display measured performance statistics and omit ambient environment values.
- **R-BENCH-004** MUST: Implement defensive fallback defaults and explicit string parsing for all accessed environment variables.
- **R-BENCH-005** MUST: Restrict reporting output strictly to benchmark timing metrics, error margins, and operation frequencies.

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