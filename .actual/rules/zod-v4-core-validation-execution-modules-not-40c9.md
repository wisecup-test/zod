# Zod Core Module Architecture and Registry Separation: Core Validation Execution Modules Not Depend

These rules are ALWAYS ACTIVE for all core schema definition, execution, parsing, check processing, error handling, metadata registry, serialization mapping, and compatibility facade integration modules.

### Rules

- **R-ZOD-001** MUST_NOT: Core validation execution modules MUST_NOT depend on outer compatibility facades, peripheral format converters, or consumer-facing legacy shims.

### Verify

```bash
# Discover and run the project static analysis and dependency linting suite from repository configuration scripts to verify unidirectional module imports.
# Discover and execute the internal architecture boundary test suite to ensure no circular references exist between core modules and compatibility layers.
```

**Accept when:**
- Static module dependency checks pass without circular dependency violations or illegal cross-boundary imports.
- Schema registry test suites confirm correct bidirectional mapping, cache invalidation, and reference resolution without memory leakage.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration checks and peer review.
</enforcement>