# node:fs Module Adoption for Protocol-Prefixed File System Operations: Consumers Validating File Contents Read Via

These rules are ALWAYS ACTIVE for all repository build scripts, release automation, code generators, and static verification scripts performing file system operations, and workspace packages executing file generation or descriptor analysis.

### Rules

- **R-NODEFS-001** MUST: Consumers validating file contents read via `node:fs` MUST enforce structured parsing and input validation before consuming data across package boundaries.

### Verify

```bash
# Discover the repository script runner and execute the module resolution linter to verify that all core imports utilize protocol prefixes.
# Discover and run the repository build validation script to ensure file system operations execute successfully across all target environments.
```

**Accept when:**
- Static analysis validates that every file system import across repository scripts utilizes the `node:fs` protocol specifier.
- All build generation and verification scripts complete without module resolution errors or unhandled file read exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>