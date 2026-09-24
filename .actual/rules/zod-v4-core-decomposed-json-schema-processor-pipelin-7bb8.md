# Zod Core Library Module: Decomposed JSON Schema Processor Pipeline and Registry Separation: Schema Transformation Processors Access Instance Metadata

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MUST: Schema transformation processors MUST access instance metadata through the centralized registry lookup abstractions rather than attaching mutable serialization state directly to schema definition instances.

### Verify

```bash
# Discover and execute the project test runner script defined in the project configuration to validate schema transformation behaviors and processor test suites.
# Execute the static type checking and modular dependency validation suites configured in the repository to guarantee unidirectional module dependencies.
# Run the repository linter and architecture boundary checks defined in project configuration to verify adherence to module import boundaries.
```

**Accept when:**
- All test suites covering schema serialization, cycle detection, and registry lookups pass with zero errors.
- Dependency verification confirms no circular dependencies exist between schema definitions and serialization processors.
- Static analysis confirms all schema types have corresponding registered transformation handlers.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>