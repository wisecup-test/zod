# Internal Core Module Architecture: Checks, Errors, and Utilities Layering: Peripheral Consumers Including Localization Bundles Compatibility

These rules are ALWAYS ACTIVE for all peripheral modules, localization bundles, compatibility adapters, and internal core submodules.

### Rules

- **R-CORE-001** MUST: Peripheral consumers including localization bundles and compatibility adapters MUST import foundational validation checks, error representations, and utility helpers directly from dedicated internal core submodules rather than monolithic barrel exports.

### Verify

```bash
# Discover and run dependency graph validation, module boundary linters, and test suites per project repository structure
```

**Accept when:**
- Static dependency analysis reports zero circular dependencies between internal core submodules and consumer modules.
- All localization modules successfully resolve imported checks, errors, and utilities from designated core subpaths.
- All unit and integration tests passing across all supported locales and compatibility facades.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis and module boundary validation enforce these rules in CI, blocking pull requests with disallowed imports or circular dependencies.
</enforcement>