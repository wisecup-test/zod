# Zod Core Library Module Decomposition: Subsystem Isolation of Schemas, Parsing, and Validation Registries: Core Validation Library Architecture Isolate Functional

These rules are ALWAYS ACTIVE for all core library validation code, schema definitions, input parsing routines, validation checks, error representations, and internal registries.

### Rules

- **R-ZOD-001** MUST: The core validation library architecture MUST isolate functional responsibilities into discrete internal modules covering schema definitions, input parsing, validation checks, error representations, and registries.
- **R-ZOD-002** MANDATORY: Execute lock-version grounding before writing code that uses a versioned library (find manifest, identify build tool, inspect lock/resolution artifact, look up official documentation for exact version, confirm APIs exist, re-run per dependency at point of use).
- **R-ZOD-003** MANDATORY: Maintain strict internal layering where foundational utilities and error definitions do not import higher-level schema constructs or parsing orchestrators.
- **R-ZOD-004** MANDATORY: Expose public capabilities through designated API facade entry points rather than allowing consumers to import internal subsystem files directly.

### Verify

```bash
# Discover the workspace task runner configuration and execute the project validation script
# (Repository-specific: e.g., pnpm run check / npm run validate)

# Inspect the root configuration to identify the static type checking task and execute it
# (Repository-specific: e.g., npx tsc --noEmit)

# Execute the discovered test execution script targeting internal module unit suites
# (Repository-specific: e.g., pnpm test)
```

**Accept when:**
- All internal module imports resolve cleanly across core subsystem boundaries without circular dependency warnings.
- Static type analysis and architectural boundary checks pass across all library modules with zero diagnostic errors.
- The discovered test suite completes with all assertions passing for schema evaluation, parsing, and error reporting.

<enforcement>
Claude Code MUST NOT skip or defer verification. Static analysis, architectural boundary linters, and mandatory peer review are strictly enforced in continuous integration pipelines. Pull requests violating module isolation or introducing circular dependencies are blocked from merging.
</enforcement>