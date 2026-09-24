# Zod Core Library Module Decomposition: Subsystem Isolation of Schemas, Parsing, and Validation Registries: Compatibility Adapters Export Core Primitives Through

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MAY: Compatibility adapters MAY re-export core primitives through transitional facades to preserve backward compatibility across major architectural iterations.

### Verify

```bash
# Discover workspace task runner and execute project validation script for module boundaries
# Discover and execute static type checking across all internal core modules
# Discover and execute internal module unit suites for parse and check subsystem behavior
```

**Accept when:**
- All internal module imports resolve cleanly across core subsystem boundaries without circular dependency warnings.
- Static type analysis and architectural boundary checks pass across all library modules with zero diagnostic errors.
- The discovered test suite completes with all assertions passing for schema evaluation, parsing, and error reporting.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via static analysis, architectural boundary linters, and architectural peer reviews.
</enforcement>