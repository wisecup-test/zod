# Zod External Core Module Delegation: Consumer Inspect Repository Lock Resolution Artifact

These rules are ALWAYS ACTIVE for all entry point modules, core module interface boundaries, and module integration modifications across package variants.

### Rules

- **R-ZOD-001** MUST: The consumer MUST inspect the repository lock or resolution artifact to determine the exact resolved dependency versions before implementing or modifying module integrations.
- **R-ZOD-002** MUST: Derive all tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-ZOD-003** MUST: Execute the LOCK-VERSION GROUNDING sequence (find dependency manifest, identify build tool, inspect repository lock/resolution artifact, look up official documentation for that exact version, confirm API existence, and re-run at point of use for version-sensitive behavior) before writing code that uses a versioned library.
- **R-ZOD-004** MUST: Ensure all published entry surfaces delegate core definitions to the external core module without local reimplementation.
- **R-ZOD-005** MUST: Verify that specialized or compact entry facades import only necessary submodules from the external module to preserve minimal footprint constraints.

### Verify

```bash
# Discover and run the project static analysis suite to verify that all entry modules import shared definitions from the external core module.
# Discover and execute the package boundary and circular dependency verification scripts from repository manifests.
# Discover and run the integration test suite to validate API compatibility across all entry facade surfaces.
```

**Accept when:**
- All published entry surfaces successfully delegate core definitions to the external core module without local reimplementation.
- Static analysis and dependency boundary checks complete with zero unresolved imports or circular references.
- All unit and integration verification suites pass across all entry point variants.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated dependency linting, architecture verification checks, and peer code review.
</enforcement>