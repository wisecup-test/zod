# fumadocs-core Source Loader Integration: Route Handlers That Serialize Documentation Downstream

These rules are ALWAYS ACTIVE for documentation workspace modules responsible for loading, indexing, or traversing page content, and route handlers and loader utilities that serialize documentation pages for downstream consumers.

### Rules

- **R-DOC-001** SHOULD: Route handlers that serialize documentation for downstream consumption SHOULD cache derived page order mappings and metadata in-memory during request processing to prevent redundant source tree traversals.

### Verify

```bash
# Discover workspace root configuration and execute documentation test suite
npm test --workspace=docs

# Run type checking across documentation modules
npm run typecheck --workspace=docs

# Execute documentation build validation script
npm run build --workspace=docs
```

**Accept when:**
- All source loader consumers and route handlers compile without type errors against the resolved source module definitions.
- Documentation endpoints successfully traverse the page hierarchy and serialize page content through the centralized source loader interface.
- Test suites validating documentation content extraction and page ordering pass with zero regressions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis and type checking in the continuous integration pipeline enforce these rules.
</enforcement>