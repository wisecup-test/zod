# Hierarchical Test Configuration Composition Using vitest/config: Package Level Test Configurations Use Mergeconfig

These rules are ALWAYS ACTIVE for all unit test runner configurations and test setup modules within workspace packages in the repository.

### Rules

- **R-TEST-001** MUST: Package-level test configurations MUST use mergeConfig to extend the shared root test configuration rather than redefining shared test runner environment settings independently.

### Verify

```bash
# Discover and run the repository test execution script across all workspace packages
# and execute the workspace-specific test script for the target package to verify the merged configuration
```

**Accept when:**
- The package test runner successfully loads the merged configuration without runtime errors.
- All unit tests in the workspace package execute and pass using the inherited and package-specific configuration options.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>