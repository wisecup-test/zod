# Zod Core Module Architecture and Registry Separation: Schema Serialization Processors Deserialization Routines Interface

These rules are ALWAYS ACTIVE for core schema definitions, execution, parsing, check processing, error handling modules, metadata registries, serialization mapping layers, and compatibility facade integrations.

### Rules

- **R-ZOD-001** SHOULD: Schema serialization processors and deserialization routines SHOULD interface with schema definitions strictly through public registry lookups and standard schema interfaces.

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