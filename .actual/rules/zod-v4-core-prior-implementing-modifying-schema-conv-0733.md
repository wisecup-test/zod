# Zod Core JSON Schema Generation and Traversal Cache Architecture: Prior Implementing Modifying Schema Conversion Modules

These rules are ALWAYS ACTIVE for core schema transformation subsystems generating standard JSON Schema artifacts from defined internal schemas, and internal processor and generator modules responsible for schema traversal, registry inspection, and check evaluation.

### Rules

- **R-ZOD-001** MUST: Prior to implementing or modifying schema conversion modules, the engineer MUST locate the repository dependency manifest and resolution artifact to verify the exact resolved version of all supporting libraries and validate API contracts against official documentation.

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
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration pipelines and architectural and peer code reviews.
</enforcement>