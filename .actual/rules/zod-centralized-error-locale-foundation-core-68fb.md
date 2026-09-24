# Zod Core Module Architecture: Centralized Error and Locale Foundation: Core Foundation Modules Not Depend Higher

These rules are ALWAYS ACTIVE for internal library modules, parsing helper functions, and facade components within the validation engine requiring error modeling, localization, or core utility primitives.

### Rules

- **R-ZOD-CORE-001** MUST_NOT: Core foundation modules MUST NOT depend on higher-level schema combinators, external facades, or downstream helper modules, preserving strict unidirectional dependency flow.

### Verify

```bash
# Discover the project script definitions and execute the repository type-checking suite to verify module boundary compliance.
# Discover and run the project test execution runner to ensure error generation and localization resolution pass all suite checks.
# Discover the repository static analysis and linting scripts to verify import directionality and module dependency constraints.
```

**Accept when:**
- The discovered type verification and test execution suites pass with zero errors across all core module consumers.
- Import analysis confirms all schema parsing and helper modules import error types and locale definitions strictly from the designated core module boundary.
- No circular dependencies exist between core foundation modules and downstream helper or facade modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>