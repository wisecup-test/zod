# Zod Core Library Modular Architecture: Engineers Consult Repository Dependency Manifest Inspect

These rules are ALWAYS ACTIVE for internal core subsystems of the library responsible for parsing, schema representation, validation assertions, and error formatting.

### Rules

- **R-ZOD-001** MUST: Engineers MUST consult the repository dependency manifest and inspect the authoritative lock artifact to determine the exact resolved dependency versions prior to integrating or modifying external standard specifications or library interfaces.

### Verify

```bash
# Discover and run project static analysis, linting, type-checking, and unit test suites
# (Commands must be discovered from the repository manifest and package configuration)
```

**Accept when:**
- All unit and contract test suites execute successfully without errors or regressions.
- Static analysis and dependency linters report zero circular dependencies across internal core modules.
- Type checking passes with zero diagnostics across all internal core module interfaces.

<enforcement>
Claude Code MUST NOT skip or defer verification. All internal core module changes must be checked against dependency manifests and verified using the repository's automated testing and linting tools.
</enforcement>