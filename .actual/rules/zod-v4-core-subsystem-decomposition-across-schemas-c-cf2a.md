# Zod Core Library Module: Subsystem Decomposition Across Schemas, Checks, and Registries: Core Schema Instances Provide Standard Compliant

These rules are ALWAYS ACTIVE for all core library modules responsible for schema definition, parsing, validation checks, error dispatch, and schema registries.

### Rules

- **R-ZOD-001** SHOULD: Core schema instances SHOULD provide standard schema compliant contracts to guarantee cross-library interoperability through standardized validation protocols.
- **R-ZOD-002** MANDATORY: The consumer MUST discover dependency management tools, build systems, lock files, and exact version requirements from the project repository rather than relying on assumed or hardcoded versions.
- **R-ZOD-003** MANDATORY: Before writing code using a versioned library, inspect the dependency manifest, identify the build tool, check the repository lock or resolution artifact for exact versions, verify via public documentation, and confirm API existence.
- **R-ZOD-004** MANDATORY: Maintain clear interface contracts between schema definition objects and the check execution subsystem to ensure check functions remain pure and stateless.
- **R-ZOD-005** MANDATORY: Verify that all internal core module interactions reference abstract interfaces rather than private internal implementation details.

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
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration checks and mandatory architectural peer reviews on pull requests modifying internal core module boundaries.
</enforcement>