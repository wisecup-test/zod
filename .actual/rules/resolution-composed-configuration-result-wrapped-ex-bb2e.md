# Hierarchical Test Configuration Composition Using vitest/config: Composed Configuration Result Wrapped Exported Defineconfig

These rules are ALWAYS ACTIVE for unit test runner configurations and test runner setup modules extending repository-wide test execution settings within workspace packages.

### Rules

- **R-VITEST-001** MUST: The composed configuration result MUST be wrapped and exported using defineConfig from vitest/config.

### Verify

```bash
# Discover and run the repository test execution script declared in the root dependency manifest across all workspace packages
# Execute the workspace-specific test script for the target package to verify that merged configuration loads and executes tests successfully
```

**Accept when:**
- The package test runner successfully loads the merged configuration from vitest/config without runtime errors.
- All unit tests in the workspace package execute and pass using the inherited and package-specific configuration options.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>