# Adoption of next/image for Documentation Asset Rendering: Provide Descriptive Alternative Text Appropriate Accessibility

These rules are ALWAYS ACTIVE for all rendering raster images, branding logos, and content illustrations within documentation UI components and layouts.

### Rules

- **R-DOC-001** MUST: Provide descriptive alternative text or appropriate accessibility labels for all rendered image elements.

### Verify

```bash
# Discover and run the repository linter to detect unoptimized image tag usage
# Discover and execute the repository type checker to validate image component properties
# Discover and execute the repository build script to confirm asset resolution and compilation integrity
```

**Accept when:**
- All image rendering in documentation presentation components passes automated lint and static analysis without unoptimized image violations
- Type verification succeeds across all component properties consuming the image module
- Repository build verification completes without missing asset or unresolved component errors

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>