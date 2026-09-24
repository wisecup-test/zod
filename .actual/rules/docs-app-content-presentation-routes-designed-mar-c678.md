# fumadocs-ui Layout Adoption for Documentation and Content Presentation: Content Presentation Routes Designed Marketing Landing

These rules are ALWAYS ACTIVE for route layout components serving documentation, blog, or content landing pages within the documentation application, and shared configuration modules defining application-wide navigation, branding, and layout properties.

### Rules

- **R-FUMA-001** MUST: Content presentation routes designed for marketing, landing, or publication streams MUST consume home layout primitives from fumadocs-ui/layouts/home.

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
Claude Code MUST NOT skip or defer verification. Pull request checks fail when route layout boundaries implement redundant custom navigation chrome instead of fumadocs-ui layout components.
</enforcement>