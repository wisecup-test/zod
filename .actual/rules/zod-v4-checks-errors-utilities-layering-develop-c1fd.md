# Internal Core Module Architecture: Checks, Errors, and Utilities Layering: Developers Inspect Authoritative Project Dependency Lock

These rules are ALWAYS ACTIVE for all localization bundles, backward-compatibility adapters, and internal core submodules.

### Rules

- **R-CORE-001** MUST: Developers MUST inspect the authoritative project dependency lock artifact to determine the exact resolved versions of all internal and external dependencies before modifying or adding consumer modules.
- **R-CORE-002** MUST: Peripheral modules (such as localization dictionaries and compatibility adapters) MUST import only dedicated checks, errors, and utility subpaths required for compilation, avoiding unified library entry points or barrel imports.
- **R-CORE-003** MUST: Developers MUST maintain strict separation between error type definitions, validation assertion checks, and general utilities to preserve modular consumption across all localization targets.

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
Claude Code MUST NOT skip or defer verification. Automated static module boundary validation, circular dependency detection, and peer code review enforce compliance.
</enforcement>