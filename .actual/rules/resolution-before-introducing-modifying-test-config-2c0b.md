# Hierarchical Test Configuration Composition Using vitest/config: Before Introducing Modifying Test Configuration Dependencies

These rules are ALWAYS ACTIVE for all unit test runner configurations for workspace packages within the repository and test runner setup modules extending repository-wide test execution settings.

### Rules

- **R-TEST-001** MUST: Before introducing or modifying test configuration dependencies, engineers MUST discover the repository lock artifact and verify the exact resolved version against the dependency manifest.
- **R-TEST-002** MUST: Import defineConfig and mergeConfig from vitest/config alongside the shared root test configuration when creating package-level test configuration modules.
- **R-TEST-003** MUST: Ensure that package-specific overrides passed to mergeConfig supply only the delta needed for the package test suite.

### Verify

```bash
# Discover and run the repository test execution script declared in the root dependency manifest across all workspace packages.
# Execute the workspace-specific test script for the target package to verify that merged configuration loads and executes tests successfully.
```

**Accept when:**
- The package test runner successfully loads the merged configuration from vitest/config without runtime errors.
- All unit tests in the workspace package execute and pass using the inherited and package-specific configuration options.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>