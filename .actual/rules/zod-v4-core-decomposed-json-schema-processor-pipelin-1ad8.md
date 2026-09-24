# Zod Core Library Module: Decomposed JSON Schema Processor Pipeline and Registry Separation: Modular Generator Coordinators Dispatch Type Specific

These rules are ALWAYS ACTIVE for internal core library modules implementing schema transformations, serialization pipelines, metadata registries, and structural traversal subsystems.

### Rules

- **R-ZOD-001** SHOULD: Modular generator coordinators SHOULD dispatch type-specified serialization tasks to dedicated processor handlers matching each schema definition category.

### Verify

```bash
# Discover and execute the project test runner script defined in project configuration
# Execute static type checking and modular dependency validation suites
# Run repository linter and architecture boundary checks
```

**Accept when:**
- All test suites covering schema serialization, cycle detection, and registry lookups pass with zero errors.
- Dependency verification confirms no circular dependencies exist between schema definitions and serialization processors.
- Static analysis confirms all schema types have corresponding registered transformation handlers.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration checks and peer code review.
</enforcement>