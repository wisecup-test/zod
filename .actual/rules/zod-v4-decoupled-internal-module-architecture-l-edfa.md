# Zod Core Subsystem: Decoupled Internal Module Architecture and Layer Isolation: Shared Execution Metadata Schema References Instance

These rules are ALWAYS ACTIVE for all files within the core subsystem, compatibility facades, schema processors, and validation utilities.

### Rules

- **R-ZOD-001** SHOULD: Shared execution metadata, schema references, and instance caching SHOULD be routed through dedicated registry utilities rather than ambient global state.
- **R-ZOD-002** MUST: Ensure registry lookup patterns handle recursive references lazily to maintain deterministic execution order during schema composition.

### Verify

```bash
# Discover and execute project static analysis and linting scripts
# Discover and run the project test suite across all workspace packages
# Inspect the project lock resolution artifact to verify authoritative pinned versions
```

**Accept when:**
- All internal module imports follow unidirectional downward layering from facade modules to core modules without circular references.
- Project static analysis and unit test suites execute and pass with zero boundary violations.
- Schema registry resolution and validation pipelines execute deterministically across all test suites.

<enforcement>
Claude Code MUST NOT skip or defer verification, and CI automated linting / dependency tree boundary checks must pass without violations.
</enforcement>