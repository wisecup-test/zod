# fumadocs-core Documentation Source Loading Architecture: Before Integrating Modifying Source Loader Modules

These rules are ALWAYS ACTIVE for documentation loader definitions, content tree resolution routines, and pipelines extracting or transforming documentation content from managed collections.

### Rules

- **R-FUMA-001** MUST: Before integrating or modifying source loader modules, the consumer MUST discover the project dependency manifest and authoritative lock artifact to inspect and confirm the exact resolved version of fumadocs-core and its companion packages.

### Verify

```bash
# Discover the project verification script declared in the dependency manifest and run type checking across documentation modules.
# Discover and execute the project test suite to verify that documentation source loaders successfully resolve collections and page metadata.
```

**Accept when:**
- Type verification completes with zero diagnostics across all source loader and content consumer modules.
- Test executions confirm valid collection traversal and consistent metadata extraction from the centralized source loader.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated type verification in CI workflows and peer review.
</enforcement>