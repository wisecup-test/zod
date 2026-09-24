# Zod Core Library Modular Architecture: Internal Core Validation Checks Define Localized

These rules are ALWAYS ACTIVE for internal core subsystems of the library responsible for parsing, schema representation, validation assertions, and error formatting.

### Rules

- **R-ZOD-CORE-001** MAY: Internal core validation checks MAY define localized regular expression constants within dedicated pattern modules when reusable across multiple check routines.

### Verify

```bash
# Discover and run static analysis and linting scripts to verify internal module dependency boundaries and detect circular references.
# Discover and run type-checking and unit test suites to validate core parsing, check execution, and error formatting integrity.
```

**Accept when:**
- All unit and contract test suites execute successfully without errors or regressions.
- Static analysis and dependency linters report zero circular dependencies across internal core modules.
- Type checking passes with zero diagnostics across all internal core module interfaces.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks and peer code reviews enforce these boundaries.
</enforcement>