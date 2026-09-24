# Zod Core Library Module: Decomposed JSON Schema Processor Pipeline and Registry Separation: Base Schema Definition Modules Not Import

These rules are ALWAYS ACTIVE for internal core library modules implementing schema transformations, serialization pipelines, metadata registries, and subsystems performing structural traversal and external schema generation on core schema instances.

### Rules

- **R-ZOD-001** MUST_NOT: Base schema definition modules MUST NOT import downstream serialization processors or schema generation coordinators, preserving unidirectional dependency flow from serializers to core schemas.

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
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration checks executing repository test and validation scripts, and peer code review verifying adherence to processor isolation and context management constraints.
</enforcement>