# fumadocs-ui Layout Adoption for Documentation and Content Presentation: Route Layout Modules Responsible Documentation Content

These rules are ALWAYS ACTIVE for route layout modules, documentation, blog, and content presentation pages within the documentation application.

### Rules

- **R-FUMA-001** MUST: Route layout modules responsible for documentation and content presentation MUST adopt standardized layout components from the fumadocs-ui library rather than constructing bespoke navigation chrome.

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
Claude Code MUST NOT skip or defer verification. Automated static analysis, type-checking, and build verification ensure route layout boundaries comply with fumadocs-ui layout adoption standards.
</enforcement>