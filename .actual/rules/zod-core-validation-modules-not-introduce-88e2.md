# Zod Core Library Modular Architecture: Core Validation Modules Not Introduce Circular

These rules are ALWAYS ACTIVE for all internal core library files responsible for parsing, schema representation, validation assertions, and error formatting.

### Rules

- **R-ZOD-MOD-001** MUST_NOT: Core validation modules MUST NOT introduce circular import dependencies across internal core module boundaries.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify internal module dependency boundaries and detect circular references.
# Discover and run the project type-checking and unit test suites to validate core parsing, check execution, and error formatting integrity.
# (Run project-specific lint, typecheck, and test commands discovered from package.json)
```

**Accept when:**
- All unit and contract test suites execute successfully without errors or regressions.
- Static analysis and dependency linters report zero circular dependencies across internal core modules.
- Type checking passes with zero diagnostics across all internal core module interfaces.

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests introducing circular dependencies or violating module segregation boundaries must be blocked and rejected until refactored.
</enforcement>