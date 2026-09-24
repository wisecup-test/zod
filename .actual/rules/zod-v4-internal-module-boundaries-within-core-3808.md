# Zod Core Module Architecture and Registry Separation: Internal Module Boundaries Within Core Architecture

These rules are ALWAYS ACTIVE for all core schema definition, execution, parsing, check processing, error handling, metadata registries, serialization mapping layers, and compatibility facade integration modules.

### Rules

- **R-ZOD-001** MUST: Internal module boundaries within the core architecture MUST maintain unidirectional dependency flows from utility and error foundations toward parsing engines and check pipelines.
- **R-ZOD-002** MUST: Implement metadata registries using bidirectional mapping structures that associate schema objects with string identifiers while providing symmetric deletion operations.
- **R-ZOD-003** MUST: Ensure compatibility modules import core functionality strictly through designated entrypoints without referencing deep internal implementation modules.

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