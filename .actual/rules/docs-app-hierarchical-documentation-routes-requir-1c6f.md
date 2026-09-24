# fumadocs-ui Layout Adoption for Documentation and Content Presentation: Hierarchical Documentation Routes Requiring Structured Tree

These rules are ALWAYS ACTIVE for all route layout components serving documentation, blog, or content landing pages within the documentation application, as well as shared configuration modules defining application-wide navigation, branding, and layout properties.

### Rules

- **R-DOC-001** MUST: Hierarchical documentation routes requiring structured tree navigation, sidebar items, and table of contents components MUST consume documentation layout primitives from fumadocs-ui/layouts/docs.

### Verify

```bash
# Discover and execute the repository type-checking script to verify interface compatibility between route layout boundaries and fumadocs-ui layout exports.
# Discover and execute the repository static analysis suite to verify absence of disallowed custom layout wrappers on documentation routes.
# Discover and execute the repository build script to confirm successful compilation of all route layout boundaries.
```

**Accept when:**
- Documentation route layouts successfully render navigation, sidebars, and body content using fumadocs-ui layout components without layout structural errors.
- All layout components resolve their configuration and source definitions through the standardized shared application configuration contract.
- The repository static verification suite passes without module resolution or layout contract violations.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis and continuous integration type-checking ensure route layout boundaries import designated fumadocs-ui layout modules.
</enforcement>