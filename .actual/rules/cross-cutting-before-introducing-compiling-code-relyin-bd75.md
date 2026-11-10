---
version: 2
name: cross-cutting-before-introducing-compiling-code-relyin-bd75
description: "Adoption of React as Core UI Component Library: Before Introducing Compiling Code Relying React"
metadata:
  actual:
    adr_id: bd758cae-ba07-4bd4-881b-eff09148593e
    status: accepted
    candidate_group_id: b06f414d-38f9-4b85-bef7-5ca278d92919
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
      - components/**
      - loaders/**
---

# Adoption of React as Core UI Component Library: Before Introducing Compiling Code Relying React

Scope: applies to `packages/docs/app/**`, `packages/docs/components/**`, `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-REACT-001** MUST: Before introducing or compiling code relying on React dependencies, developers MUST discover the ecosystem lock artifact and verify the exact resolved library version according to the Discovery Policy.

### Verify

```bash
# Discover the repository build script from the dependency manifest and execute the static type verification.
# Inspect project configuration to identify and run the static linter verifying component hook constraints and client directive compliance.
```

**Accept when:**
- All component modules pass static type checking without missing dependency declarations.
- Component lint verification passes with zero violations of hook rules and rendering boundary constraints.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>