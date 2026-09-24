# Zod Core JSON Schema Generation and Traversal Cache Architecture: Traversal Context Attach Custom Metadata Parent

These rules are ALWAYS ACTIVE for all core schema transformation subsystems and internal processor/generator modules generating standard JSON Schema artifacts.

### Rules

- **R-ZOD-001** MAY: The traversal context MAY attach custom metadata or parent boundary flags to generated schema structures to facilitate downstream post-processing.

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
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipelines validate unit tests and recursive schema edge cases, and pull requests bypassing context cache checks will be blocked.
</enforcement>