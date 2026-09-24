# metabench Internal Module Adoption: Shared Benchmark Utility Routines Interface Directly

These rules are ALWAYS ACTIVE for all performance evaluation test suites, benchmark suites, and benchmark modules measuring data validation, transformation, and parse operations within the repository.

### Rules

- **R-META-001** MUST: All shared benchmark utility routines MUST interface directly with the standardized harness lifecycle hooks rather than defining independent timer mechanisms.

### Verify

```bash
# Discover the project benchmark script defined in the dependency manifest and execute it to run all performance suites.
# Inspect the build and lint scripts in the repository configuration to verify static module boundary compliance across benchmark suites.
```

**Accept when:**
- All benchmark suites execute successfully through the standardized harness runner without unhandled lifecycle rejections.
- Static boundary checks confirm benchmark suites rely solely on authorized internal harness and utility modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>