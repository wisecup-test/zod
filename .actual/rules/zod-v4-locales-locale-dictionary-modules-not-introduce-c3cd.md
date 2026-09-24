# Zod Core Internal Module Partitioning for Locale Definitions: Locale Dictionary Modules Not Introduce Cyclical

These rules are ALWAYS ACTIVE for all localization dictionary modules, language locale files, and internal core interface consumptions within the validation library package.

### Rules

- **R-ZOD-LOCALE-001** MUST_NOT: Locale dictionary modules MUST NOT introduce cyclical dependencies by importing parser engines, composite schema builders, or top-level validator singletons.
- **R-ZOD-LOCALE-002** MUST: Import only check descriptors, error types, and formatting utility helpers from internal core submodules when creating a new locale module.
- **R-ZOD-LOCALE-003** MUST: Use standardized utility formatting functions rather than custom string concatenation for all error messages parameterized with input values or type expectations.

### Verify

```bash
# Discover and execute the localization test suite
# Discover the project module boundary linter and execute static dependency analysis
# Discover the build script from the package configuration and execute a production compile
```

**Accept when:**
- All locale definitions compile cleanly and pass their respective message formatting test cases.
- Dependency linting confirms that localization modules import only designated internal core submodules without circular dependencies.
- Module bundle inspection verifies that importing an individual locale dictionary does not pull in unreferenced schema parsers.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis, module boundary lint rules, and pull request code reviews enforce these requirements.
</enforcement>