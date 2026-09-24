# Zod Core Module Architecture: Centralized Error and Locale Foundation: Before Consuming Extending Versioned Library Dependencies

These rules are ALWAYS ACTIVE for internal library modules, parsing helper functions, and facade components within the validation engine requiring error modeling, localization, or core utility primitives.

### Rules

- **R-ZOD-001** MUST: Before consuming or extending versioned library dependencies, the engineering team MUST discover the repository dependency manifest and resolution artifact to verify the exact locked version and validate that core module exports conform to that recorded resolution.

### Verify

```bash
# Discover and execute project type-checking suite
# Discover and run test execution runner
# Discover and run static analysis and linting scripts
```

**Accept when:**
- The discovered type verification and test execution suites pass with zero errors across all core module consumers.
- Import analysis confirms all schema parsing and helper modules import error types and locale definitions strictly from the designated core module boundary.
- No circular dependencies exist between core foundation modules and downstream helper or facade modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated type checking, architectural boundary analysis, and peer code review.
</enforcement>