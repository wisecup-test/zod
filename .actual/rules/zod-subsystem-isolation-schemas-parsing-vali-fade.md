# Zod Core Library Module Decomposition: Subsystem Isolation of Schemas, Parsing, and Validation Registries: Internal Schema Definitions Delegate Validation Checks

These rules are ALWAYS ACTIVE for internal core library modules, schema definitions, parse runners, validation checks, and error formatting modules.

### Rules

- **R-ZOD-001** MUST: Internal schema definitions MUST delegate validation checks to dedicated check subsystems and error construction to dedicated error modules rather than implementing embedded validation routines or direct error instantiations.
- **R-ZOD-002** MUST: Maintain strict internal layering where foundational utilities and error definitions do not import higher-level schema constructs or parsing orchestrators.
- **R-ZOD-003** MUST: Expose public capabilities through designated API facade entry points rather than allowing consumers to import internal subsystem files directly.
- **R-ZOD-004** MUST: Execute the dependency manifest discovery, build tool identification, and lock file resolution sequence before importing or using versioned library components.

### Verify

```bash
# Discover workspace task runner and execute project validation script for module boundaries
# (Project-specific task runner command to be used, e.g., pnpm validate or npm run check-boundaries)

# Execute static type checking task across all internal core modules
# (Project-specific typecheck command to be used, e.g., npx tsc --noEmit)

# Execute unit test suites targeting parse and check subsystems
# (Project-specific test command to be used, e.g., npx vitest run)
```

**Accept when:**
- All internal module imports resolve cleanly across core subsystem boundaries without circular dependency warnings.
- Static type analysis and architectural boundary checks pass across all library modules with zero diagnostic errors.
- The discovered test suite completes with all assertions passing for schema evaluation, parsing, and error reporting.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via static analysis, architectural boundary linters, and test execution pipelines.
</enforcement>