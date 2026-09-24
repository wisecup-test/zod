# Adoption of the @/loaders/source Centralized Content Source Loader Module: Transformations Targeting Downstream Representations Such Search

These rules are ALWAYS ACTIVE for all documentation pages, blog views, layout wrappers, search API handlers, text generation utilities consuming content collections, and any new route or endpoint requiring access to structured content, navigation trees, or content metadata.

### Rules

- **R-SRC-001** SHOULD: Transformations targeting downstream representations such as search indices or structured text outputs SHOULD derive their base collections directly from the centralized source loader module to maintain parity with rendered pages.

### Verify

```bash
# Discover and run the project type-checking script defined in the root configuration
# Discover and run the repository test suite
# Discover and execute the repository static analysis and linting scripts
```

**Accept when:**
- The project type-checking and static analysis scripts pass with zero errors across all content-consuming routes.
- All documentation, blog, search, and text export routes successfully resolve content through the centralized source loader module.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>