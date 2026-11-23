---
version: 2
name: cross-cutting-core-validation-architecture-isolate-jso-586b
description: "Zod Core JSON Schema Transformation Modules: Core Validation Architecture Isolate Json Schema"
metadata:
  actual:
    adr_id: 586bbef5-54fc-4bbc-887a-6c6eb84d628c
    status: accepted
    candidate_group_id: bf562f7e-2eba-4e98-a358-82c1dab13f6c
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# Zod Core JSON Schema Transformation Modules: Core Validation Architecture Isolate Json Schema

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for:
- Core schema transformation and JSON Schema generation modules within the library.
- Context management, schema processor registries, and metadata lookup implementations.

### Rules

- **R-LM-001** MUST: The core validation architecture MUST isolate JSON Schema translation into modular processors coordinated through an explicit traversal context.

### Verify

- Discover the repository configuration to locate and execute the test runner targeting core schema conversion modules.
- Discover the workspace static analysis and linting scripts to verify compliance with internal module dependency boundaries.

**Accept when:**

- The repository test suite executes without failures across all JSON Schema generation scenarios, including recursive and circular definitions.
- Static boundary checks confirm schema transformation processors only interact with core registries through the context interface.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated unit and integration test suites validating schema-to-JSON-Schema conversions.
- Verified by: Static analysis and code review inspecting module import boundaries and context threading.
- Violation handling: Pull requests bypassing the traversal context or directly coupling schema definitions to serialization logic are rejected during code review.
- Exception process: Exceptions for specialized schema transformations must be submitted to the core architecture maintainers with technical justification demonstrating why context-based dispatch is infeasible.
</enforcement>
