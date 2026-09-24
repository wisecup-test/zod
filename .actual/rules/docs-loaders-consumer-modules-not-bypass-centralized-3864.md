# fumadocs-core Documentation Source Loading Architecture: Consumer Modules Not Bypass Centralized Source

These rules are ALWAYS ACTIVE for documentation loader definitions, content tree resolution routines, and pipelines extracting or transforming documentation content from managed collections.

### Rules

- **R-DOC-001** MUST_NOT: Consumer modules MUST NOT bypass the centralized source loader to execute direct, unindexed file reads for documentation pages that exist within the managed source tree.

### Verify

```bash
# Discover the project verification script declared in the dependency manifest and run type checking across documentation modules.
# Discover and execute the project test suite to verify that documentation source loaders successfully resolve collections and page metadata.
```

**Accept when:**
- Type verification completes with zero diagnostics across all source loader and content consumer modules.
- Test executions confirm valid collection traversal and consistent metadata extraction from the centralized source loader.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated type verification in CI workflows and peer review verifying that documentation content access routes through the standardized source loader.
</enforcement>