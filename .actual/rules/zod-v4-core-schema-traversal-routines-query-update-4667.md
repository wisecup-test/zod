# Zod Core JSON Schema Generation and Traversal Cache Architecture: Schema Traversal Routines Query Update Identity

These rules are ALWAYS ACTIVE for core schema transformation subsystems generating standard JSON Schema artifacts from defined internal schemas, internal processor and generator modules responsible for schema traversal, registry inspection, and check evaluation.

### Rules

- **R-ZOD-001** MUST: Schema traversal routines MUST query and update an identity cache within the traversal context prior to processing any schema definition to prevent infinite loops on recursive references and prevent duplicate definition generation.

### Verify

```bash
# Discover and run the project test suite targeting schema serialization and JSON Schema generation modules.
# Discover and execute the type-checking and linter suites to verify module contracts and boundary conformance across core libraries.
```

**Accept when:**
- All unit tests covering schema-to-JSON-Schema conversion, including cyclic and recursive schema test suites, pass without regression.
- Traversal context properly records visited schemas and prevents duplicate definition output.
- Static analysis and type validation pass with zero errors across all core modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests touching core schema generation or processor modules must undergo architectural and peer code reviews, and violations will block merging.
</enforcement>