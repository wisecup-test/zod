# Internal Core Module Architecture: Checks, Errors, and Utilities Layering: Consumer Modules Requiring Error Code Definitions

These rules are ALWAYS ACTIVE for localization bundles, backward-compatibility layers, and peripheral consumer modules requiring access to common error definitions, assertion checks, and utility primitives.

### Rules

- **R-CORE-001** SHOULD: Consumer modules requiring error code definitions and validation messages SHOULD bind exclusively to the dedicated error contracts and utility interfaces exposed by the core modules.

### Verify

```bash
# Discover and run the project repository dependency graph validation script to ensure no circular dependencies exist
# Discover and run the project repository static analysis and module boundary linter
# Discover and execute the project repository test suite
```

**Accept when:**
- Static dependency analysis reports zero circular dependencies between internal core submodules and consumer modules.
- All localization modules successfully resolve imported checks, errors, and utilities from designated core subpaths.
- All unit and integration tests passing across all supported locales and compatibility facades.

<enforcement>
Automated static module boundary validation and circular dependency detection scripts enforce these boundaries in CI pipelines, and Claude Code MUST NOT introduce disallowed import paths or circular module dependencies.
</enforcement>