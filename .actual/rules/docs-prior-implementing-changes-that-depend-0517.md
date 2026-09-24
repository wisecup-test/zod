# Adoption of the @/loaders/source Centralized Content Source Loader Module: Prior Implementing Changes That Depend Versioned

These rules are ALWAYS ACTIVE for all documentation pages, blog views, layout wrappers, search API handlers, text generation utilities, and any new route or endpoint requiring access to structured content, navigation trees, or content metadata.

### Rules

- **R-SRC-001** MUST: Prior to implementing changes that depend on versioned content processing or source integration libraries, developers MUST discover the dependency manifest and authoritative lock artifact to confirm the exact resolved versions and API specifications.

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
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration checks executing repository linting, type validation, and test suites on pull requests, and peer code review.
</enforcement>