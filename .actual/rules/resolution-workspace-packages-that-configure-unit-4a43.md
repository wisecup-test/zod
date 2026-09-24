# Hierarchical Test Configuration Composition Using vitest/config: Workspace Packages That Configure Unit Testing

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-VIT-001** MUST: Workspace packages that configure unit testing suites MUST define their configuration by importing defineConfig and mergeConfig from vitest/config and merging package-level options with the shared root test configuration module.

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