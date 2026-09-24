# fumadocs-core Source Loader Integration: Content Endpoints Transformation Utilities Not Bypass

These rules are ALWAYS ACTIVE for documentation workspace modules responsible for loading, indexing, or traversing page content, and route handlers and loader utilities that serialize documentation pages for downstream consumers.

### Rules

- **R-FUMADOCS-001** MUST_NOT: Content endpoints and transformation utilities MUST NOT bypass the fumadocs-core/source abstraction to read raw content files directly, except when loading companion metadata artifacts defined outside the page tree schema.

### Verify

```bash
# Discover workspace root configuration and run documentation test suite
# Run type checker across documentation modules to validate source loader call signatures
# Execute documentation build validation script
```

**Accept when:**
- All source loader consumers and route handlers compile without type errors against the resolved source module definitions.
- Documentation endpoints successfully traverse the page hierarchy and serialize page content through the centralized source loader interface.
- Test suites validating documentation content extraction and page ordering pass with zero regressions.

<enforcement>
Claude Code MUST NOT skip or defer verification. Direct filesystem parsing or bypassing the central source loader must be blocked.
</enforcement>