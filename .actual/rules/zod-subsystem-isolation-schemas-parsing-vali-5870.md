# Zod Core Library Module Decomposition: Subsystem Isolation of Schemas, Parsing, and Validation Registries: Input Parsing Pipelines Coordinate Passes Through

These rules are ALWAYS ACTIVE for all internal core modules, schema definitions, parse runners, validation checks, and error formatting modules.

### Rules

- **R-ZOD-001** MUST: Input parsing pipelines MUST coordinate parsing passes through dedicated parse utilities while remaining decoupled from concrete schema construction APIs.

### Verify

```bash
# Discover workspace task runner and run validation
# Run static type checking across all internal core modules
# Execute unit tests targeting internal module suites
```

**Accept when:**
- All internal module imports resolve cleanly across core subsystem boundaries without circular dependency warnings.
- Static type analysis and architectural boundary checks pass across all library modules with zero diagnostic errors.
- The discovered test suite completes with all assertions passing for schema evaluation, parsing, and error reporting.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by static analysis, architectural boundary linters, and mandatory architectural peer reviews in CI pipelines.
</enforcement>