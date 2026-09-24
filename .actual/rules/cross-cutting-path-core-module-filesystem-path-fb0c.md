# node:path Core Module for Filesystem Path Resolution: Before Implementing Updating Modules That Rely

These rules are ALWAYS ACTIVE for all repository maintenance scripts, configuration definitions, test suites, and workspace components or utility modules requiring filesystem path creation, navigation, or verification.

### Rules

- **R-PATH-001** MUST: Before implementing or updating modules that rely on runtime dependencies, developers MUST inspect the repository lock artifact and dependency manifest to verify the resolved runtime version compatibility.
- **R-PATH-002** MUST: Ensure all module specifiers utilize the protocol prefix (e.g., node:path) when accessing core runtime modules.
- **R-PATH-003** MUST: When resolving paths relative to current module files, convert module location URLs to system paths prior to passing them into path calculation methods.

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
Claude Code MUST NOT skip or defer verification. Continuous integration pipelines, static analysis rules, and peer code reviews enforce these requirements, and violations will block pull request merging.
</enforcement>