# Zod Core Internal Module Partitioning for Locale Definitions: Localization Definitions Zod Library Import Exclusively

These rules are ALWAYS ACTIVE for all localization modules and internal core submodules within the validation library package.

### Rules

- **R-ZOD-LOC-001** MUST: Localization definitions in the Zod library MUST import exclusively from dedicated internal core submodules providing check descriptors, error types, and formatting utility functions, and MUST NOT depend on the root library export or schema construction modules.

### Verify

```bash
# Discover and run the project test runner for the localization test suite
# Discover and run the module boundary linter to verify no circular or monolithic imports exist
# Discover and run the build script to verify production bundle decoupling
```

**Accept when:**
- All locale definitions compile cleanly and pass their respective message formatting test cases.
- Dependency linting confirms that localization modules import only designated internal core submodules without circular dependencies.
- Module bundle inspection verifies that importing an individual locale dictionary does not pull in unreferenced schema parsers.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated static analysis, module boundary lint rules, and maintainer pull request code reviews.
</enforcement>