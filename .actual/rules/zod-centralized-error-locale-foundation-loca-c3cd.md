# Zod Core Module Architecture: Centralized Error and Locale Foundation: Localization Messages Default Error Map Bindings

These rules are ALWAYS ACTIVE for internal library modules, parsing helper functions, and facade components within the validation engine requiring error modeling, localization, or core utility primitives.

### Rules

- **R-ZOD-001** MUST: Localization messages and default error map bindings MUST route through centralized locale definitions provided by the core module to maintain consistent message formatting across all parsing contexts.

### Verify

```bash
# Discover and execute project type-checking script
# Discover and execute project test execution runner
# Discover and execute repository static analysis and linting scripts
```

**Accept when:**
- The discovered type verification and test execution suites pass with zero errors across all core module consumers.
- Import analysis confirms all schema parsing and helper modules import error types and locale definitions strictly from the designated core module boundary.
- No circular dependencies exist between core foundation modules and downstream helper or facade modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated type checking, architectural boundary analysis, and peer code review enforce adherence to core module import conventions.
</enforcement>