# node:path Core Module for Filesystem Path Resolution: Developers Not Use Manual String Concatenation

These rules are ALWAYS ACTIVE for all repository maintenance scripts, configuration definitions, test suites, and workspace components requiring filesystem path creation, navigation, or verification.

### Rules

- **R-PATH-001** MUST_NOT: Developers MUST NOT use manual string concatenation or hardcoded directory separators to construct filesystem paths.
- **R-PATH-002** MUST: Ensure all module specifiers utilize the protocol prefix (`node:`) when accessing core runtime modules.
- **R-PATH-003** MUST: Convert module location URLs to system paths prior to passing them into path calculation methods when resolving paths relative to current module files.

### Verify

```bash
# Discover and execute the repository test suite through the configured test runner script
# Run project static analysis and linting verification scripts to check for un-prefixed core module imports and path concatenations
# Execute project build and resolution scripts to verify cross-platform path resolution across workspace packages
```

**Accept when:**
- All repository test suites and verification scripts pass without path resolution errors.
- Static analysis confirms zero un-prefixed core module imports and zero manual path concatenations/hardcoded separators across repository scripts and configurations.
- Path resolution tests succeed consistently across both POSIX and Windows runtime environments.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration pipelines, static analysis, linting, and peer code reviews enforce protocol-prefixed imports and portable path operations, blocking non-compliant pull requests.
</enforcement>