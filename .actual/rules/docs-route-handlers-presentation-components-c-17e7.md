# Adoption of the @/loaders/source Centralized Content Source Loader Module: Route Handlers Presentation Components Consume Pre

These rules are ALWAYS ACTIVE for all documentation pages, blog views, layout wrappers, search API handlers, text generation utilities, and any new routes or endpoints requiring access to structured content, navigation trees, or content metadata.

### Rules

- **R-SRC-001** SHOULD: Route handlers and presentation components SHOULD consume pre-aggregated source collections and tree structures exposed by the source loader module rather than performing ad-hoc content filtering or tree transformations.

### Verify

```bash
# Discover and run the project type-checking script defined in the root configuration to verify all consumers adhere to the source loader interface.
# Discover and run the repository test suite to confirm source resolution, page tree generation, and search indexing pass without regression.
# Discover and execute the repository static analysis and linting scripts to verify compliance with the source loader import boundary.
```

**Accept when:**
- The project type-checking and static analysis scripts pass with zero errors across all content-consuming routes.
- All documentation, blog, search, and text export routes successfully resolve content through the centralized source loader module.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks execute repository linting, type validation, and test suites on pull requests.
</enforcement>