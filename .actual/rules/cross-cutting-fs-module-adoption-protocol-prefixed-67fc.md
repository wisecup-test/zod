# node:fs Module Adoption for Protocol-Prefixed File System Operations: Codebases Not Import File System Capabilities

These rules are ALWAYS ACTIVE for all repository build scripts, release automation, code generators, static verification scripts, and workspace packages executing file generation or descriptor analysis.

### Rules

- **R-FS-001** MUST_NOT: Codebases MUST NOT import file system capabilities using bare, un-prefixed module specifiers.

### Verify

```bash
# Discover the repository script runner and execute the module resolution linter to verify that all core imports utilize protocol prefixes.
# Discover and run the repository build validation script to ensure file system operations execute successfully across all target environments.
```

**Accept when:**
- Static analysis validates that every file system import across repository scripts utilizes the node:fs protocol specifier.
- All build generation and verification scripts complete without module resolution errors or unhandled file read exceptions.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>