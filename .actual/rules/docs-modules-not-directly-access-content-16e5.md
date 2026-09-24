# Adoption of the @/loaders/source Centralized Content Source Loader Module: Modules Not Directly Access Content Storage

These rules are ALWAYS ACTIVE for all documentation pages, blog views, layout wrappers, search API handlers, text generation utilities, and any new route or endpoint requiring access to structured content, navigation trees, or content metadata.

### Rules

- **R-SRC-001** MUST_NOT: Modules MUST_NOT directly access content storage mechanisms, read filesystem paths, or configure independent content source loaders outside of the centralized source loader interface.

### Verify

```bash
# Discover and run the project type-checking script defined in the root configuration
# Discover and run the repository test suite to confirm source resolution
# Discover and execute the repository static analysis and linting scripts
```

**Accept when:**
- The project type-checking and static analysis scripts pass with zero errors across all content-consuming routes.
- All documentation, blog, search, and text export routes successfully resolve content through the centralized source loader module.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>