# Zod Core Library Module: Subsystem Decomposition Across Schemas, Checks, and Registries: Validation Checks Constraint Predicates Encapsulated Dedicated

These rules are ALWAYS ACTIVE for all core library modules responsible for schema definition, parsing, validation checks, error dispatch, and schema registries.

### Rules

- **R-ZOD-001** MUST: Validation checks and constraint predicates MUST be encapsulated in the dedicated checks module, isolating evaluation logic from schema type definition structures.

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
Claude Code MUST NOT skip or defer verification. All core module interactions must reference abstract interfaces rather than private internal implementation details, and pull requests violating module encapsulation boundaries are blocked from merging.
</enforcement>