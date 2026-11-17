---
version: 2
name: cross-cutting-editorial-landing-blog-sub-routes-a222
description: "Adoption of fumadocs-ui Layout Components for Documentation Route Shells: Editorial Landing Blog Sub Routes Use"
metadata:
  actual:
    adr_id: a222b225-ef9a-4cac-aab5-3fbf6488e9b9
    status: accepted
    candidate_group_id: 3eda226b-0493-41c6-8697-5bf32b4fdf24
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
---

# Adoption of fumadocs-ui Layout Components for Documentation Route Shells: Editorial Landing Blog Sub Routes Use

Scope: applies to `packages/docs/app/**`.

These rules are ALWAYS ACTIVE for all route layout modules governing documentation, technical guides, reference material, and content publishing sections.

### Rules

- **R-ADR-001** SHOULD: Editorial, landing, or blog sub-routes SHOULD use the specialized home layout component from fumadocs-ui to maintain visual continuity with documentation while presenting open-format content.

### Verify

```bash
# Discover the repository build and static analysis scripts declared in the project manifest, and execute type-checking and build verification
# Example discovery and execution (derive actual commands from package manifest):
# npm run typecheck
# npm run build
```

**Accept when:**
- Static type analysis passes with zero errors across all documentation route layout modules.
- Documentation and content route layouts render navigation headers, sidebars, and main content containers without runtime exceptions.
- All route layout implementations ingest the centralized layout configuration module without local duplication of global navigation structures.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks and peer code reviews verify compliance, and pull requests violating these standards without an approved exception will be blocked from merging.
</enforcement>