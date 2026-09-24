# Zod Core Module Architecture and Registry Separation: Schema Metadata Associations Identifier Lookups Serialization

These rules are ALWAYS ACTIVE for core schema definition, execution, parsing, check processing, error handling modules, metadata registries, serialization mapping layers, and compatibility facade integrations.

### Rules

- **R-ZOD-001** MUST: Schema metadata associations, schema identifier lookups, and serialization mappings MUST be managed through dedicated bidirectional registries rather than attaching arbitrary mutable properties directly to schema instances.

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