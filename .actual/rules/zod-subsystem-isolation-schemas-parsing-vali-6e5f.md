# Zod Core Library Module Decomposition: Subsystem Isolation of Schemas, Parsing, and Validation Registries: When Consuming Extending Versioned Library Dependencies

These rules are ALWAYS ACTIVE for internal schema definitions, parse runners, validation checks, error formatting modules, and when consuming or extending versioned library dependencies.

### Rules

- **R-ZOD-001** MUST: When consuming or extending versioned library dependencies, inspect the authoritative dependency lock artifact to determine the exact resolved dependency version prior to implementation.
- **R-ZOD-002** MUST: Maintain strict internal layering where foundational utilities and error definitions do not import higher-level schema constructs or parsing orchestrators.
- **R-ZOD-003** MUST: Expose public capabilities through designated API facade entry points rather than allowing consumers to import internal subsystem files directly.

### Verify

```bash
# Discover workspace task runner configuration and execute project validation script
# Identify root configuration, static type checking task, and execute across internal core modules
# Execute discovered test execution script targeting internal module unit suites
```

**Accept when:**
- All internal module imports resolve cleanly across core subsystem boundaries without circular dependency warnings.
- Static type analysis and architectural boundary checks pass across all library modules with zero diagnostic errors.
- The discovered test suite completes with all assertions passing for schema evaluation, parsing, and error reporting.

<enforcement>
Claude Code MUST NOT skip or defer verification. Violation handling: Pull requests violating internal module isolation or introducing circular dependencies are blocked from merging.
</enforcement>