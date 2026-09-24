# Zod Core Subsystem: Decoupled Internal Module Architecture and Layer Isolation: When Integrating Versioned Third Party Workspace

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** MUST: When integrating versioned third-party or workspace dependencies, the consumer MUST inspect repository lock or resolution artifacts to verify the authoritative resolved version before implementation.

### Verify

```bash
# Discover and execute the project static analysis and linting scripts
# Discover and run the project test suite across all workspace packages
# Inspect the project lock resolution artifact to verify pinned versions
```

**Accept when:**
- All internal module imports follow unidirectional downward layering from facade modules to core modules without circular references.
- Project static analysis and unit test suites execute and pass with zero boundary violations.
- Schema registry resolution and validation pipelines execute deterministically across all test suites.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>