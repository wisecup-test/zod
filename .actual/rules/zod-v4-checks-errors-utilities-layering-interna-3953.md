# Internal Core Module Architecture: Checks, Errors, and Utilities Layering: Internal Core Submodules Not Establish Upward

These rules are ALWAYS ACTIVE for all localization bundles, backward-compatibility adapters, and internal core submodules in the project.

### Rules

- **R-CORE-001** MUST_NOT: Internal core submodules MUST NOT establish upward dependencies on localization modules, compatibility layers, or peripheral consumers.
- **R-CORE-002** MUST: Maintain strict separation between error type definitions, validation assertion checks, and general utilities to preserve modular consumption across all localization targets.
- **R-CORE-003** MUST: Verify when introducing a new locale bundle or adapter module that imports reference only the dedicated checks, errors, and utility subpaths required for message compilation.

### Verify

```bash
# Discover and run the project repository dependency graph validation script to ensure no circular dependencies exist between core submodules and peripheral consumers.
# Discover and run the project repository static analysis and module boundary linter to verify that localization modules import only permitted core submodules.
# Discover and execute the project repository test suite to validate that all localization and compatibility modules compile and execute against core contracts.
```

**Accept when:**
- Static dependency analysis reports zero circular dependencies between internal core submodules and consumer modules.
- All localization modules successfully resolve imported checks, errors, and utilities from designated core subpaths.
- All unit and integration tests passing across all supported locales and compatibility facades.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static module boundary validation, circular dependency detection scripts, and peer code reviews enforce compliance.
</enforcement>