# Zod Core Library Modular Architecture: Standard Schema Specification Adapters Isolated Within

These rules are ALWAYS ACTIVE for internal core subsystems of the library responsible for parsing, schema representation, validation assertions, and error formatting.

### Rules

- **R-ZOD-001** SHOULD: Standard schema specification adapters SHOULD be isolated within dedicated boundary modules to decouple third-party interoperability contracts from internal parsing mechanics.

### Verify

```bash
# Discover and run project static analysis, dependency boundary linters, type-checking, and test suites
npm run lint
npm run typecheck
npm test
```

**Accept when:**
- All unit and contract test suites execute successfully without errors or regressions.
- Static analysis and dependency linters report zero circular dependencies across internal core modules.
- Type checking passes with zero diagnostics across all internal core module interfaces.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration checks executing dependency boundary linters and type checkers, and peer code review.
</enforcement>