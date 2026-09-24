# metabench Internal Module Adoption: Benchmark Suites Isolate Setup Sample Generation

These rules are ALWAYS ACTIVE for all performance evaluation test suites, benchmark suites, and modules measuring data validation, transformation, and parse operations within the repository.

### Rules

- **R-MB-001** SHOULD: Benchmark suites SHOULD isolate benchmark setup and sample generation from timed evaluation routines orchestrated by the harness.

### Verify

```bash
# Discover and execute the project benchmark script defined in the dependency manifest
# Inspect the build and lint scripts in the repository configuration to verify static module boundary compliance
```

**Accept when:**
- All benchmark suites execute successfully through the standardized harness runner without unhandled lifecycle rejections.
- Static boundary checks confirm benchmark suites rely solely on authorized internal harness and utility modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>