# json-schema-processors Internal Module Adoption for Schema Transformation: Schema Transformation Architecture Adopt Json Processors

These rules are ALWAYS ACTIVE for all schema transformation and core generator code files within the project.

### Rules

- **R-JSP-001** MUST: The schema transformation architecture MUST adopt the json-schema-processors internal module to isolate individual schema definition conversions from top-level schema generation.

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
Claude Code MUST NOT skip or defer verification.
</enforcement>