# Zod Core Internal Module Partitioning for Locale Definitions: Locale Message Formatters Rely Internal Core

These rules are ALWAYS ACTIVE for all code implementing or maintaining language locale modules within the validation library package.

### Rules

- **R-ZOD-LOC-001** SHOULD: Locale message formatters SHOULD rely on internal core utility helpers for text interpolation and value serialization rather than introducing disparate helper utilities.

### Verify

```bash
# Discover and execute the localization test suite
# Discover the project module boundary linter and execute static dependency analysis
# Discover the build script and execute a production compile to verify bundle decoupling
```

**Accept when:**
- All locale definitions compile cleanly and pass their respective message formatting test cases.
- Dependency linting confirms that localization modules import only designated internal core submodules without circular dependencies.
- Module bundle inspection verifies that importing an individual locale dictionary does not pull in unreferenced schema parsers.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated static analysis, module boundary lint rules, and test suite execution during CI/CD and pull request reviews.
</enforcement>