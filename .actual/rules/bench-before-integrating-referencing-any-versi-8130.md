# metabench Internal Module Adoption: Before Integrating Referencing Any Versioned Dependency

These rules are ALWAYS ACTIVE for performance evaluation test suites, benchmark suites, and benchmark modules measuring data validation, transformation, and parse operations within the repository.

### Rules

- **R-META-001** MUST: Before integrating or referencing any versioned dependency in benchmark suites, consumers MUST inspect the repository lock artifact to verify the exact resolved version against authorized dependency ranges.
- **R-META-002** MUST: Discover the project benchmark script defined in the dependency manifest and execute it to run all performance suites.
- **R-META-003** MUST: Inspect the build and lint scripts in the repository configuration to verify static module boundary compliance across benchmark suites.

### Verify

```bash
# Find the dependency manifest, inspect the lock artifact, and run project benchmark/lint scripts
# Example discovery verification loop:
# 1. Locate manifest and lock artifact
# 2. Run benchmark script defined in manifest
# 3. Run build/lint scripts to check module boundaries
```

**Accept when:**
- All benchmark suites execute successfully through the standardized harness runner without unhandled lifecycle rejections.
- Static boundary checks confirm benchmark suites rely solely on authorized internal harness and utility modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>