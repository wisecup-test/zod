# json-schema-processors Internal Module Adoption for Schema Transformation: Processors Map Validation Checks Standardized Schema

These rules are ALWAYS ACTIVE for internal modules implementing schema-to-schema transformation within the core library, including processors and generators handling schema serialization and validation keyword mapping.

### Rules

- **R-PROC-001** SHOULD: Processors map validation checks to standardized schema validation keywords by delegating to dedicated check evaluation helpers.
- **R-PROC-002** MUST: Processors be authored as pure functional mappings accepting the schema definition, traversal context, and options.
- **R-PROC-003** MUST: Ensure the context seen cache key identity relies on schema definition object references to accurately detect recursive cycles.
- **R-PROC-004** MUST: Execute lock-version grounding before writing code that uses a versioned library: find dependency manifest, identify build tool, inspect lock/resolution artifact for exact version, look up official docs for that exact version, confirm APIs exist, and re-run per dependency at point of use.

### Verify

```bash
# Discover the project test runner script from the root package manifest and execute the core test suite covering schema transformation.
# Inspect the build configuration to identify and run the type-checking and linting verification tasks across core modules.
```

**Accept when:**
- All unit tests covering schema transformation processors and generator pipelines execute successfully without regression.
- Cyclic schema references resolve to valid references without triggering call stack exceptions.
- Static type analysis and module linting checks pass with zero reported errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration pipeline executing unit tests and static analysis, and mandatory peer code review for changes affecting core schema transformation modules.
</enforcement>