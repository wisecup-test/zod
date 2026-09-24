# node:path Core Module for Filesystem Path Resolution: Implementations Use Normalize Node Path Sanitize

These rules are ALWAYS ACTIVE for all repository maintenance scripts, configuration definitions, and test suites executing in the project environment, as well as any workspace component or utility module requiring filesystem path creation, navigation, or verification.

### Rules

- **R-PATH-001** MAY: Implementations MAY use normalize from node:path to sanitize user-provided or externally sourced relative path inputs before resolution.
- **R-PATH-002** MANDATORY: Ensure all module specifiers utilize the protocol prefix when accessing core runtime modules.
- **R-PATH-003** MANDATORY: When resolving paths relative to current module files, convert module location URLs to system paths prior to passing them into path calculation methods.
- **R-PATH-004** MANDATORY: Execute lock-version grounding before writing code that uses a versioned library (find manifest, identify build tool, inspect lock artifact for resolved version, look up official version-specific docs, confirm API existence, re-run per dependency at point of use).

### Verify

```bash
# Discover and execute the repository test suite through the configured test runner script in the project manifest
# Run the project static analysis and linting verification scripts to check for un-prefixed core module imports
# Execute the project build and resolution scripts to verify cross-platform path resolution across workspace packages
```

**Accept when:**
- All repository test suites and verification scripts pass without path resolution errors.
- Static analysis confirms zero un-prefixed core module imports across repository scripts and configurations.
- Path resolution tests succeed consistently across both POSIX and Windows runtime environments.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration pipelines, static analysis rules, and code reviews enforce protocol-prefixed core module imports and block non-portable path operations.
</enforcement>