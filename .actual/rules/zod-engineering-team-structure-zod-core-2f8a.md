# Zod Core Library Modular Architecture: Engineering Team Structure Zod Core Library

These rules are ALWAYS ACTIVE for internal core subsystems of the library responsible for parsing, schema representation, validation assertions, and error formatting.

### Rules

- **R-ZOD-001** MUST: Structure the Zod core library into discrete, specialized internal modules that segregate schema representation, parsing logic, validation checks, regular expressions, and error handling into dedicated compilation units.
- **R-ZOD-002** MUST: Maintain unidirectional module imports across internal boundaries to ensure tree-shakability and prevent circular dependency cycles.
- **R-ZOD-003** MUST: Execute lock-version grounding steps before writing code that uses a versioned library (discover manifest, build tool, exact resolved version from lock, version-specific docs/API confirmation).

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify internal module dependency boundaries and detect circular references.
# Discover and run the project type-checking and unit test suites to validate core parsing, check execution, and error formatting integrity.
```

**Accept when:**
- All unit and contract test suites execute successfully without errors or regressions.
- Static analysis and dependency linters report zero circular dependencies across internal core modules.
- Type checking passes with zero diagnostics across all internal core module interfaces.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>