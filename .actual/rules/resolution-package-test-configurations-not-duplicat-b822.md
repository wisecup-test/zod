# Hierarchical Test Configuration Composition Using vitest/config: Package Test Configurations Not Duplicate Shared

These rules are ALWAYS ACTIVE for all unit test runner configurations for workspace packages within the repository and test runner setup modules extending repository-wide test execution settings.

### Rules

- **R-TEST-001** MUST_NOT: Package test configurations MUST NOT duplicate shared global test runner settings that are already declared within the shared root configuration module.

### Verify

```bash
# Discover and run the repository test execution script declared in the root dependency manifest across all workspace packages
# Execute the workspace-specific test script for the target package to verify that merged configuration loads and executes tests successfully
```

**Accept when:**
- The package test runner successfully loads the merged configuration without runtime errors.
- All unit tests in the workspace package execute and pass using the inherited and package-specific configuration options.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>