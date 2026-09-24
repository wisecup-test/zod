# Zod Core Module Architecture: Centralized Error and Locale Foundation: Parsing Transformation Utilities Remain Stateless Helper

These rules are ALWAYS ACTIVE for internal library modules, parsing helper functions, and facade components within the validation engine requiring error modeling, localization, or core utility primitives.

### Rules

- **R-ZOD-001** SHOULD: Parsing and transformation utilities SHOULD remain stateless helper functions that accept input data and validation contexts while delegating issue accumulation and failure creation to core error constructs.

### Verify

```bash
# Discover and execute project type-checking, test execution, and static analysis/linting suites according to the repository configuration.
```

**Accept when:**
- The discovered type verification and test execution suites pass with zero errors across all core module consumers.
- Import analysis confirms all schema parsing and helper modules import error types and locale definitions strictly from the designated core module boundary.
- No circular dependencies exist between core foundation modules and downstream helper or facade modules.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>