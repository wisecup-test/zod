# Hierarchical Test Configuration Composition Using vitest/config: Package Configurations Limit Overrides Strictly Specific

These rules are ALWAYS ACTIVE for unit test runner configurations and test setup modules for workspace packages within the repository.

### Rules

- **R-TEST-001** SHOULD: Package configurations limit overrides strictly to package-specific scope, such as package root directories, mock setups, or test include filters.

### Verify

```bash
# Discover and run the repository test execution script declared in the root dependency manifest across all workspace packages.
# Execute the workspace-specific test script for the target package to verify that merged configuration loads and executes tests successfully.
```

**Accept when:**
- The package test runner successfully loads the merged configuration without runtime errors.
- All unit tests in the workspace package execute and pass using the inherited and package-specific configuration options.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>