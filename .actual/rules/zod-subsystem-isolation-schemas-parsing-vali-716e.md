# Zod Core Library Module Decomposition: Subsystem Isolation of Schemas, Parsing, and Validation Registries: Internal Core Modules Not Introduce Circular

These rules are ALWAYS ACTIVE for all implementation and extension of internal schema definitions, parse runners, validation checks, error formatting modules, and architecture boundary definitions between public library APIs, compatibility wrappers, and internal core subsystems.

### Rules

- **R-ZOD-001** MUST_NOT: Internal core modules MUST NOT introduce circular module dependencies between schema declarations, parsing routines, and public API factories.
- **R-ZOD-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-ZOD-003** MANDATORY: Before writing code that uses a versioned library, execute the lock-version grounding steps in order (find dependency manifest, identify build tool, inspect lock/resolution artifact, lookup official documentation for exact version, confirm every API/class/function exists in that version, re-run per dependency at point of use).
- **R-ZOD-004** MUST: Maintain strict internal layering where foundational utilities and error definitions do not import higher-level schema constructs or parsing orchestrators.
- **R-ZOD-005** MUST: Expose public capabilities through designated API facade entry points rather than allowing consumers to import internal subsystem files directly.

### Verify

```bash
# Discover the workspace task runner configuration and execute the project validation script
# Inspect the root configuration to identify the static type checking task and execute it across all internal core modules
# Execute the discovered test execution script targeting internal module unit suites
```

**Accept when:**
- All internal module imports resolve cleanly across core subsystem boundaries without circular dependency warnings.
- Static type analysis and architectural boundary checks pass across all library modules with zero diagnostic errors.
- The discovered test suite completes with all assertions passing for schema evaluation, parsing, and error reporting.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by static analysis and architectural boundary linters executed in continuous integration pipelines, as well as mandatory architectural peer review on changes affecting core module exports and internal boundary contracts.
</enforcement>