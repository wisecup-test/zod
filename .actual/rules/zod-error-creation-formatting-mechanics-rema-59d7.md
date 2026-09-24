# Zod Core Library Modular Architecture: Error Creation Formatting Mechanics Remain Decoupled

These rules are ALWAYS ACTIVE for internal core subsystems of the library responsible for parsing, schema representation, validation assertions, and error formatting.

### Rules

- **R-ZOD-001** SHOULD: Error creation and formatting mechanics SHOULD remain decoupled from parsing control flows, exposing structured error objects through dedicated error definition interfaces.
- **R-ZOD-002** MANDATORY: Organize internal core logic into focused, single-responsibility modules, keeping utilities and error types independent of higher-level parsing orchestration.
- **R-ZOD-003** MANDATORY: Maintain unidirectional module imports across internal boundaries to ensure tree-shakability and prevent circular dependency cycles.
- **R-ZOD-004** MANDATORY: Execute lock-version grounding before writing code that uses a versioned library: find dependency manifest, identify build tool, inspect lock/resolution artifact for exact version, check official documentation/changelog for that exact version, confirm API existence, and re-run per dependency at point of use.

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