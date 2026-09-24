# json-schema-processors Internal Module Adoption for Schema Transformation: Before Introducing Modifying Dependencies Related Schema

These rules are ALWAYS ACTIVE for internal modules implementing schema-to-schema transformation within the core library, as well as processors and generators handling schema serialization and validation keyword mapping.

### Rules

- **R-JSON-001** MUST: Before introducing or modifying dependencies related to schema transformation modules, the consumer MUST inspect the project lock artifact to resolve the authoritative pinned dependency versions.

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