# Zod Core Library Module: Subsystem Decomposition Across Schemas, Checks, and Registries: Zod Core Library Implementations Decompose Validation

These rules are ALWAYS ACTIVE for all core library modules responsible for schema definition, parsing, validation checks, error dispatch, and schema registries.

### Rules

- **R-ZOD-001** MUST: Zod Core library implementations MUST decompose validation runtime primitives into dedicated internal modules separating schema definitions, check assertions, error tracking, registry metadata, parsing routines, and standard schema interoperability.

### Verify

```bash
# Discover and execute the repository dependency boundary verification script to ensure internal core module isolation.
# Discover and run the project test suite covering core schema execution, check validation, and registry caching.
# Discover and run the repository type-checking and linting workflows to verify interface adherence across all sub-modules.
```

**Accept when:**
- All core module unit and integration tests execute successfully without failure.
- Static analysis confirms zero circular dependencies between internal core library modules.
- Registry operations correctly store, retrieve, and delete schema instances without memory leakage.

<enforcement>
Claude Code MUST NOT skip or defer verification. All changes must adhere to module encapsulation boundaries, and code violating registry isolation or error handling contracts must be refactored before approval.
</enforcement>