# Zod Core JSON Schema Generation and Traversal Cache Architecture: Json Schema Generation Subsystem Isolate Generator

These rules are ALWAYS ACTIVE for all core schema transformation subsystems, internal processor modules, and generator modules responsible for schema traversal, registry inspection, and check evaluation.

### Rules

- **R-ZOD-GEN-001** MUST: The JSON Schema generation subsystem MUST isolate generator orchestration, processor dispatch, and registry lookups into distinct cohesive modules coordinated through a shared traversal context.

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
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipelines validate unit tests and recursive schema edge cases, and architectural and peer code reviews enforce compliance.
</enforcement>