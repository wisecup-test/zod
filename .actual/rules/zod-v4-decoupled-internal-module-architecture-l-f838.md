# Zod Core Subsystem: Decoupled Internal Module Architecture and Layer Isolation: Internal Core Submodules Not Establish Circular

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MUST_NOT: Internal core submodules MUST_NOT establish circular import paths or execute cross-submodule side effects during module initialization.

### Verify

```bash
# Discover and execute the project static analysis and linting scripts to verify that module dependency boundaries and import directions adhere to architectural constraints.
# Discover and run the project test suite across all workspace packages to ensure cross-module compatibility and validation parity.
# Inspect the project lock resolution artifact to verify that all referenced dependencies match the authoritative pinned versions.
```

**Accept when:**
- All internal module imports follow unidirectional downward layering from facade modules to core modules without circular references.
- Project static analysis and unit test suites execute and pass with zero boundary violations.
- Schema registry resolution and validation pipelines execute deterministically across all test suites.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>