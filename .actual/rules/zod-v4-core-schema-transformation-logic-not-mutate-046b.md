# Zod Core JSON Schema Generation and Traversal Cache Architecture: Schema Transformation Logic Not Mutate Incoming

These rules are ALWAYS ACTIVE for core schema transformation subsystems, internal processor, and generator modules responsible for schema traversal, registry inspection, and check evaluation.

### Rules

- **R-ZOD-001** SHOULD_NOT: Schema transformation logic SHOULD NOT mutate incoming schema definitions or global registry tables during context traversal.

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
Claude Code MUST NOT skip or defer verification. Verification is mandatory for all core schema generation and processor modules.
</enforcement>