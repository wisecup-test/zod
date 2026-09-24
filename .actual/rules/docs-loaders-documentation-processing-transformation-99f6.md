# fumadocs-core Documentation Source Loading Architecture: Documentation Processing Transformation Pipelines Consume Source

These rules are ALWAYS ACTIVE for all documentation subsystems, loader modules, and transformation pipelines consuming source tree nodes and page metadata.

### Rules

- **R-SRC-001** SHOULD: Documentation processing and transformation pipelines SHOULD consume source tree nodes and page metadata directly from the source loader abstraction.
- **R-SRC-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-SRC-003** MANDATORY: Before writing code that uses a versioned library, execute lock-version grounding in order: find dependency manifest, identify build tool, inspect lock/resolution artifact for exact version, look up official documentation for that exact version, confirm every API exists in that exact version, and re-run steps per dependency at point of use for version-sensitive behavior.

### Verify

```bash
# Discover and run the project type verification script across documentation modules
# Discover and execute the project test suite to verify documentation source loaders resolve collections and metadata
```

**Accept when:**
- Type verification completes with zero diagnostics across all source loader and content consumer modules.
- Test executions confirm valid collection traversal and consistent metadata extraction from the centralized source loader.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated type verification and peer review block pull requests introducing direct file reads or ad-hoc markdown parsing for documentation pages.
</enforcement>