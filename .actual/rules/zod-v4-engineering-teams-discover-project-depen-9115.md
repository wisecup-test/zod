# Zod Core Module Architecture and Registry Separation: Engineering Teams Discover Project Dependency Manifest

These rules are ALWAYS ACTIVE for all core schema definition, execution, parsing, check processing, error handling modules, metadata registries, serialization mapping layers, and compatibility facade integrations.

### Rules

- **R-ZOD-001** MUST: Engineering teams MUST discover the project dependency manifest and resolve the exact locked version from the repository resolution artifact prior to implementing or consuming library primitives.

### Verify

```bash
# Discover and run the project static analysis and dependency linting suite from repository configuration scripts to verify unidirectional module imports.
# Discover and execute the internal architecture boundary test suite to ensure no circular references exist between core modules and compatibility layers.
```

**Accept when:**
- Static module dependency checks pass without circular dependency violations or illegal cross-boundary imports.
- Schema registry test suites confirm correct bidirectional mapping, cache invalidation, and reference resolution without memory leakage.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>