# Zod Core Module Architecture: Centralized Error and Locale Foundation: Modules Providing Runtime Schema Evaluation Parsing

These rules are ALWAYS ACTIVE for internal library modules, parsing helper functions, and facade components within the validation engine requiring error modeling, localization, or core utility primitives.

### Rules

- **R-ZOD-CORE-001** MUST: Modules providing runtime schema evaluation, parsing helpers, and public facades MUST import core error structures, default localization mappings, and shared foundational utilities exclusively from the centralized Zod core module rather than re-declaring error classes or formatting logic locally.

### Verify

```bash
# Discover and execute project type-checking suite
# Discover and execute test runner
# Discover and execute static analysis and linting scripts
```

**Accept when:**
- The discovered type verification and test execution suites pass with zero errors across all core module consumers.
- Import analysis confirms all schema parsing and helper modules import error types and locale definitions strictly from the designated core module boundary.
- No circular dependencies exist between core foundation modules and downstream helper or facade modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated type checking, static analysis, and review mechanisms will block pull requests introducing circular dependencies, locally duplicated error structures, or bypassed core locale maps.
</enforcement>