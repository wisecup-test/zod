# metabench Internal Module Adoption: Benchmark Suites Not Introduce External Microbenchmarking

These rules are ALWAYS ACTIVE for performance evaluation test suites, benchmark suites, and benchmark modules measuring data validation, transformation, and parse operations within the repository.

### Rules

- **R-META-001** MUST_NOT: Benchmark suites MUST NOT introduce external microbenchmarking runners or ad-hoc timing loops that bypass the internal metabench harness interface.

### Verify

```bash
# Discover and execute the project benchmark script defined in the dependency manifest
# Inspect build and lint scripts to verify static module boundary compliance across benchmark suites
```

**Accept when:**
- All benchmark suites execute successfully through the standardized harness runner without unhandled lifecycle rejections.
- Static boundary checks confirm benchmark suites rely solely on authorized internal harness and utility modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>