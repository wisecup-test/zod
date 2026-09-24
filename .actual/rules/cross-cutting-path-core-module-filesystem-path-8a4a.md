# node:path Core Module for Filesystem Path Resolution: Source Modules Performing Filesystem Path Operations

These rules are ALWAYS ACTIVE for all source modules performing filesystem path operations, repository maintenance scripts, configuration definitions, and test suites executing in the project environment.

### Rules

- **R-PATH-001** MUST: Source modules performing filesystem path operations MUST import filesystem utilities using the explicit node:path module specifier rather than un-prefixed module identifiers.

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