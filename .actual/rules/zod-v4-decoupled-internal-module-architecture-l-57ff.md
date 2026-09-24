# Zod Core Subsystem: Decoupled Internal Module Architecture and Layer Isolation: Core Schema Primitives Execution Checks Error

These rules are ALWAYS ACTIVE for all implementation of internal schema validation logic, constraint checking, error formatting, and serialization within the core subsystem, as well as authoring compatibility facades, adapters, and schema processor extensions.

### Rules

- **R-ZOD-001** MUST: Core schema primitives, execution checks, error formats, and shared registries MUST reside in decoupled internal submodules that isolate their internal state and export minimal functional contracts.

### Verify

```bash
# Discover and execute project static analysis and linting scripts
# Discover and run project test suites
# Inspect project lock resolution artifacts
```

**Accept when:**
- All internal module imports follow unidirectional downward layering from facade modules to core modules without circular references.
- Project static analysis and unit test suites execute and pass with zero boundary violations.
- Schema registry resolution and validation pipelines execute deterministically across all test suites.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration automated linting, dependency tree boundary checks, and peer code review mandatory approval enforce these rules.
</enforcement>