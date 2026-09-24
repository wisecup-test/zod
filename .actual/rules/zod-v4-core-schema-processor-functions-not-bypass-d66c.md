# Zod Core JSON Schema Generation and Traversal Cache Architecture: Schema Processor Functions Not Bypass Shared

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MUST_NOT: Schema processor functions MUST NOT bypass the shared context cache or directly invoke recursive root generator routines without propagating the active visited registry.

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
Claude Code MUST NOT skip or defer verification. Violation handling: Pull requests bypassing context cache checks or breaking modular separation will be blocked at review; failures in recursive schema tests will trigger immediate build failure.
</enforcement>