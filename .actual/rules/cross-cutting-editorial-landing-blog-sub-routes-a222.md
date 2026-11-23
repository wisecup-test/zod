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

These rules are ALWAYS ACTIVE for:
- Route layout modules governing documentation, technical guides, reference material, and content publishing sections.

### Rules

- **R-LM-001** SHOULD: Editorial, landing, or blog sub-routes SHOULD use the specialized home layout component from fumadocs-ui to maintain visual continuity with documentation while presenting open-format content.

### Verify

- Discover the repository build and static analysis scripts declared in the project manifest, and execute the type-checking pipeline to confirm layout component type conformance.
- Discover and execute the project test runner to verify that route layout components render with required configuration properties.
- Inspect layout imports across documentation route hierarchies to confirm layout components are sourced from fumadocs-ui layout entry points and bind to the centralized configuration module.

**Accept when:**

- Static type analysis passes with zero errors across all documentation route layout modules.
- Documentation and content route layouts render navigation headers, sidebars, and main content containers without runtime exceptions.
- All route layout implementations ingest the centralized layout configuration module without local duplication of global navigation structures.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration checks executing static type analysis and application build verification.
- Verified by: Peer code review for all pull requests that introduce or modify route layout modules.
- Violation handling: Pull requests that implement custom layout shells for documentation or blog routes without utilizing fumadocs-ui layout primitives or an approved exception will be blocked from merging.
- Exception process: Submit an exception request detailing the structural layout incompatibility to the architecture and documentation platform leads for review.
</enforcement>
