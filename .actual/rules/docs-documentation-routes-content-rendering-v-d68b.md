# Adoption of the @/loaders/source Centralized Content Source Loader Module: Documentation Routes Content Rendering Views Search

These rules are ALWAYS ACTIVE for all documentation routes, content rendering views, search endpoints, plain text extractors, layout wrappers, and blog views consuming content collections.

### Rules

- **R-SRC-001** MUST: All documentation routes, content rendering views, search endpoints, and plain text extractors MUST access content collections, metadata, and page trees exclusively through the @/loaders/source internal module.

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
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks, peer code reviews, and build validation enforce compliance with the source loader import boundary.
</enforcement>