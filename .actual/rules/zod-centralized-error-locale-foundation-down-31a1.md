# Zod Core Module Architecture: Centralized Error and Locale Foundation: Downstream Helper Facade Modules Not Instantiate

These rules are ALWAYS ACTIVE for internal library modules, parsing helper functions, and facade components within the validation engine requiring error modeling, localization, or core utility primitives.

### Rules

- **R-ZOD-001** MUST_NOT: Downstream helper and facade modules MUST NOT instantiate or throw unstandardized error types, but MUST instantiate ZodError instances or delegate error formation directly to core error utilities.

### Verify

```bash
# Discover and execute repository type-checking suite
# Discover and run test execution runner
# Discover repository static analysis and linting scripts to verify import directionality
```

**Accept when:**
- The discovered type verification and test execution suites pass with zero errors across all core module consumers.
- Import analysis confirms all schema parsing and helper modules import error types and locale definitions strictly from the designated core module boundary.
- No circular dependencies exist between core foundation modules and downstream helper or facade modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>