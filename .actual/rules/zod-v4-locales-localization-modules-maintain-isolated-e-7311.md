# Zod Core Internal Module Partitioning for Locale Definitions: Localization Modules Maintain Isolated Exports Allow

These rules are ALWAYS ACTIVE for all localization modules and internal core submodules within the validation library package.

### Rules

- **R-LOC-001** SHOULD: Localization modules SHOULD maintain isolated exports to allow consumers to include individual locale dictionaries without bundling unreferenced languages or runtime parsers.
- **R-LOC-002** MUST: When creating a new locale module, import only the check descriptors, error types, and formatting utility helpers from the internal core submodules.
- **R-LOC-003** MUST: Ensure all error messages parameterized with input values or type expectations use the standardized utility formatting functions rather than custom string concatenation.

### Verify

```bash
# Discover and execute the project test runner for the localization test suite
# Discover the project module boundary linter and execute static dependency analysis to verify no circular or monolithic imports exist
# Discover the build script from the package configuration and execute a production compile to verify bundle decoupling
```

**Accept when:**
- All locale definitions compile cleanly and pass their respective message formatting test cases.
- Dependency linting confirms that localization modules import only designated internal core submodules without circular dependencies.
- Module bundle inspection verifies that importing an individual locale dictionary does not pull in unreferenced schema parsers.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis, module boundary lint rules, and pull request code reviews enforce these requirements.
</enforcement>