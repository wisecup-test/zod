# node:path Core Module for Filesystem Path Resolution: When Resolving Paths Relative Module Boundaries

These rules are ALWAYS ACTIVE for all repository maintenance scripts, configuration definitions, test suites, and workspace components or utility modules executing in the project environment requiring filesystem path creation, navigation, or verification (excluding browser-only client runtime code and pure algorithmic code operating exclusively on in-memory data structures).

### Rules

- **R-PATH-001** SHOULD: When resolving paths relative to module boundaries in module environments, implementations SHOULD combine the fileURLToPath API with dirname and resolve from node:path.
- **R-PATH-002** MANDATORY: Ensure all module specifiers utilize the protocol prefix when accessing core runtime modules.
- **R-PATH-003** MANDATORY: When resolving paths relative to current module files, convert module location URLs to system paths prior to passing them into path calculation methods.

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
Claude Code MUST NOT skip or defer verification. Verified by continuous integration pipelines, static analysis rules prohibiting un-prefixed core module imports, and peer code reviews.
</enforcement>