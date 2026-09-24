# fumadocs-core Documentation Source Loading Architecture: Documentation Loaders Integrate Companion Transformation Modules

These rules are ALWAYS ACTIVE for documentation loader definitions, content tree resolution routines, and pipelines extracting or transforming documentation content from managed collections.

### Rules

- **R-DOC-001** MAY: Documentation loaders MAY integrate companion transformation modules to process MDX syntax trees when preparing content for specialized downstream extraction.
- **R-DOC-002** MANDATORY: The consumer MUST derive all tool names, file names, commands, package managers, and version numbers from the project repository during discovery.
- **R-DOC-003** MANDATORY: Before writing code that uses a versioned library, execute in order: find dependency manifest, identify build tool, inspect repository lock or resolution artifact for exact version, look up official documentation for that exact version, confirm every API/class/function exists in that version, and re-run steps per dependency at point of use for version-sensitive behavior.

### Verify

```bash
# Discover the project verification script declared in the dependency manifest and run type checking across documentation modules.
# Discover and execute the project test suite to verify that documentation source loaders successfully resolve collections and page metadata.
```

**Accept when:**
- Type verification completes with zero diagnostics across all source loader and content consumer modules.
- Test executions confirm valid collection traversal and consistent metadata extraction from the centralized source loader.

<enforcement>
Claude Code MUST NOT skip or defer verification. Direct file reads or ad-hoc markdown parsing for documentation pages must be blocked, and violations must be refactored to consume the centralized source loader interface.
</enforcement>