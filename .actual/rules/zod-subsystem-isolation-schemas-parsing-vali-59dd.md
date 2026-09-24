# Zod Core Library Module Decomposition: Subsystem Isolation of Schemas, Parsing, and Validation Registries: Global Registries Metadata Cache Structures Accessed

These rules are ALWAYS ACTIVE for implementation and extension of internal schema definitions, parse runners, validation checks, and error formatting modules, as well as architecture boundary definitions between public library APIs, compatibility wrappers, and internal core subsystems.

### Rules

- **R-ZOD-001** SHOULD: Global registries and metadata cache structures SHOULD be accessed through designated registry boundaries rather than direct global state mutation.

### Verify

```bash
# Discover workspace task runner and execute project validation script
# Inspect root configuration for static type checking task and execute
# Execute discovered test execution script targeting internal module unit suites
```

**Accept when:**
- All internal module imports resolve cleanly across core subsystem boundaries without circular dependency warnings.
- Static type analysis and architectural boundary checks pass across all library modules with zero diagnostic errors.
- The discovered test suite completes with all assertions passing for schema evaluation, parsing, and error reporting.

<enforcement>
Claude Code MUST NOT skip or defer verification. Violation handling: Pull requests violating internal module isolation or introducing circular dependencies are blocked from merging.
</enforcement>