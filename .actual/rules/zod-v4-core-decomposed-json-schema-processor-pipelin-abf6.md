# Zod Core Library Module: Decomposed JSON Schema Processor Pipeline and Registry Separation: Json Schema Generation Procedures Maintain Explicit

These rules are ALWAYS ACTIVE for internal core library modules implementing schema transformations, serialization pipelines, metadata registries, and subsystems performing structural traversal and external schema generation on core schema instances.

### Rules

- **R-ZOD-001** MUST: JSON schema generation procedures MUST maintain an explicit traversal context containing a visited cache to register visited schema instances and prevent infinite recursion during cycle resolution.

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
Claude Code MUST NOT skip or defer verification. All pull requests introducing circular dependencies between schemas and processors will be blocked by continuous integration.
</enforcement>