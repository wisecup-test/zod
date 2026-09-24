# node:path Core Module for Filesystem Path Resolution: Filesystem Path Compositions Use Resolve Join

These rules are ALWAYS ACTIVE for all repository maintenance scripts, configuration definitions, test suites, and workspace components or utility modules requiring filesystem path creation, navigation, or verification.

### Rules

- **R-NODE-PATH-001** MUST: Filesystem path compositions MUST use the resolve or join APIs from node:path to ensure deterministic, cross-platform path construction.

### Verify

```bash
# Discover and execute the repository test suite through the configured test runner script in the project manifest.
# Run the project static analysis and linting verification scripts to check for un-prefixed core module imports.
# Execute the project build and resolution scripts to verify cross-platform path resolution across workspace packages.
```

**Accept when:**
- All repository test suites and verification scripts pass without path resolution errors.
- Static analysis confirms zero un-prefixed core module imports across repository scripts and configurations.
- Path resolution tests succeed consistently across both POSIX and Windows runtime environments.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>