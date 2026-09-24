# fumadocs-core Documentation Source Loading Architecture: Documentation Subsystem Use Fumadocs Core Source

These rules are ALWAYS ACTIVE for all documentation subsystem files, loader definitions, and content tree resolution routines.

### Rules

- **R-DOC-001** MUST: The documentation subsystem MUST use fumadocs-core/source as the authoritative abstraction for loading, indexing, and traversing documentation collections.

### Verify

```bash
# Discover the project verification script declared in the dependency manifest and run type checking across documentation modules.
# Discover and execute the project test suite to verify that documentation source loaders successfully resolve collections and page metadata.
```

**Accept when:**
- Type verification completes with zero diagnostics across all source loader and content consumer modules.
- Test executions confirm valid collection traversal and consistent metadata extraction from the centralized source loader.

<enforcement>
Claude Code MUST NOT skip or defer verification. Violation handling: Pull requests introducing direct file reads or ad-hoc markdown parsing for documentation pages must be blocked and refactored to consume the centralized source loader interface.
</enforcement>