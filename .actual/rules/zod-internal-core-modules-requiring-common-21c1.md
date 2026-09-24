# Zod Core Library Modular Architecture: Internal Core Modules Requiring Common Primitive

These rules are ALWAYS ACTIVE for internal core subsystems of the library responsible for parsing, schema representation, validation assertions, error formatting, and module boundaries linking foundational utilities to specification adapters and runtime execution pipelines.

### Rules

- **R-ZOD-001** MUST: Internal core modules requiring common primitive functions or string manipulations MUST route shared logic through dedicated utility modules rather than cross-importing unrelated domain modules.

### Verify

```bash
# Discover and run project static analysis and linting scripts to verify module dependency boundaries and detect circular references
# Discover and run project type-checking and unit test suites to validate core parsing, check execution, and error formatting integrity
```

**Accept when:**
- All unit and contract test suites execute successfully without errors or regressions.
- Static analysis and dependency linters report zero circular dependencies across internal core modules.
- Type checking passes with zero diagnostics across all internal core module interfaces.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests introducing circular dependencies or violating module segregation boundaries must be blocked and rejected until refactored.
</enforcement>