# Internal Core Module Architecture: Checks, Errors, and Utilities Layering: Subsystem Modules Requiring Composite Validation Behavior

These rules are ALWAYS ACTIVE for subsystem modules requiring composite validation behavior (such as localization dictionary modules, backward-compatibility adapters, and internal submodules requiring direct access to core checks, errors, or utility functions).

### Rules

- **R-CORE-001** MAY: Subsystem modules requiring composite validation behavior MAY import multiple specialized core submodules concurrently to satisfy check, error, and utility requirements without introducing circular links.

### Verify

```bash
# Discover and run the project repository dependency graph validation script
# Discover and run the project repository static analysis and module boundary linter
# Discover and execute the project repository test suite
```

**Accept when:**
- Static dependency analysis reports zero circular dependencies between internal core submodules and consumer modules.
- All localization modules successfully resolve imported checks, errors, and utilities from designated core subpaths.
- All unit and integration tests passing across all supported locales and compatibility facades.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static module boundary validation and circular dependency detection scripts enforce these constraints.
</enforcement>