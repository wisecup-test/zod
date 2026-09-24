# Zod Core JSON Schema Generation and Traversal Cache Architecture: Schema Specific Conversion Routines Encapsulate Default

These rules are ALWAYS ACTIVE for all core schema transformation subsystems, internal processor, and generator modules generating standard JSON Schema artifacts.

### Rules

- **R-ZOD-001** SHOULD: Schema-specific conversion routines SHOULD encapsulate default value serialization and property constraints within specialized processor units rather than in the root orchestration module.

### Verify

```bash
# Discover and run the project test suite targeting schema serialization and JSON Schema generation modules
# Discover and execute the type-checking and linter suites to verify module contracts and boundary conformance across core libraries
```

**Accept when:**
- All unit tests covering schema-to-JSON-Schema conversion, including cyclic and recursive schema test suites, pass without regression.
- Traversal context properly records visited schemas and prevents duplicate definition output.
- Static analysis and type validation pass with zero errors across all core modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory and enforced by automated continuous integration pipelines, architectural reviews, and automated recursive schema test executions.
</enforcement>