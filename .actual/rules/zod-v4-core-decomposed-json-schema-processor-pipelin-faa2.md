# Zod Core Library Module: Decomposed JSON Schema Processor Pipeline and Registry Separation: Engineering Teams Inspect Project Dependency Manifest

These rules are ALWAYS ACTIVE for internal core library modules implementing schema transformations, serialization pipelines, metadata registries, and subsystems performing structural traversal and external schema generation on core schema instances.

### Rules

- **R-ZOD-001** MUST: Engineering teams MUST inspect the project dependency manifest and resolve the exact locked version from the authoritative repository resolution artifact before implementing or modifying module integrations.
- **R-ZOD-002** MUST: Instantiate a fresh traversal context for each top-level transformation invocation, passing the context reference through child processor functions to record visited instances.
- **R-ZOD-003** MUST: Query the centralized schema registry for auxiliary metadata such as titles, descriptions, and custom keywords before emitting generated schema nodes.

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
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration checks executing repository test and validation scripts, and by peer code review verifying adherence to processor isolation and context management constraints.
</enforcement>