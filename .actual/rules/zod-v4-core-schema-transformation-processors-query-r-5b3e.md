# json-schema-processors Internal Module Adoption for Schema Transformation: Schema Transformation Processors Query Register Processed

These rules are ALWAYS ACTIVE for internal modules implementing schema-to-schema transformation within the core library, including processors and generators handling schema serialization and validation keyword mapping.

### Rules

- **R-JSP-001** MUST: Schema transformation processors MUST query and register processed schema instances in the context seen cache to detect cyclical schema references and avoid redundant processing.

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
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration pipeline executing unit tests and static analysis, and mandatory peer code review.
</enforcement>