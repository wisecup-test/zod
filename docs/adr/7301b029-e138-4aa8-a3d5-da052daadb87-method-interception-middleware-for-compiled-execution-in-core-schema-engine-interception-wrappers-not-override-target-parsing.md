---
version: 2
name: 7301b029-e138-4aa8-a3d5-da052daadb87-method-interception-middleware-for-compiled-execution-in-core-schema-engine-interception-wrappers-not-override-target-parsing
description: "Method Interception Middleware for Compiled Execution in Core Schema Engine: Interception Wrappers Not Override Target Parsing"
metadata:
  actual:
    adr_id: 7301b029-e138-4aa8-a3d5-da052daadb87
    status: accepted
    candidate_group_id: ec121c99-6a31-4a67-8d1c-83bb9701913c
    evidence:
      source: deep
  scope:
    root: packages/zod
    paths:
      - src/v4/core/**
---

# Method Interception Middleware for Compiled Execution in Core Schema Engine: Interception Wrappers Not Override Target Parsing

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/zod`

Applies to:
- `src/v4/core/**`

## Context

- High-throughput schema parsing requires fast-path execution capabilities while maintaining full fidelity with baseline dynamic validation semantics.
- Core schema objects expose standardized execution methods that consumers invoke directly, necessitating transparent acceleration at the boundary.
- Dynamic property initialization and tree mutation within core structuring helpers require isolation from prototype pollution vulnerabilities.

## Problem Statement

Accelerating schema parsing requires integrating compiled routines into existing schema instances without mutating their outward method contracts or degrading safety during dynamic property traversal and fallback evaluation.

## Decision

1. MUST_NOT: Interception wrappers MUST NOT override target parsing methods destructively without retaining an executable reference to the original source implementation.

## Policy Block

- MUST_NOT Interception wrappers MUST NOT override target parsing methods destructively without retaining an executable reference to the original source implementation.

In scope:
- Core schema parsing compilation and method installation routines.
- Internal structural tree traversal and dynamic property initialization utilities.

Out of scope:
- Consumer-facing custom transformation callbacks defined outside the core engine.
- Static validation rules that do not participate in compilation pipelines.

## Rationale

- Method interception middleware enables the engine to attach optimized execution logic onto schema instances dynamically without re-instantiating schema classes.
- Preserving references to original methods ensures that edge cases, unsupported constructs, or invalid execution outcomes can seamlessly fall back to baseline implementations.
- Defensive object property definitions in internal navigation helpers prevent unintentional prototype modifications during error structure assembly.

## Consequences

Positive:
- Enables transparent ahead-of-time execution optimization without breaking the public contract of validation methods.
- Preserves backward compatibility and robust error handling by falling back to base parsing logic when fast-path execution yields invalid signals.
- Encapsulates execution interception within a dedicated middleware layer decoupled from schema definition logic.

Negative:
- Direct method patching on target objects creates mutable interception boundaries that complicate debugging of stack traces.
- Maintaining dual execution paths between compiled fast paths and standard fallback routines increases testing surface area.
- Safeguarding object prototype modifications requires defensive accessor guards across internal structuring helpers.

## Alternatives

- Monolithic parser replacement overriding original parsing methods directly without fallback delegation (rejected)
  Rejected because: Precludes graceful fallback to standard dynamic parsing paths when ahead-of-time compilation cannot resolve complex validation rules or returns an invalid signal.
  When valid: Only viable when compilation is guaranteed to be universally exhaustive for every schema type and configuration.
- Direct schema class inheritance for compiled parsers (rejected)
  Rejected because: Increases prototype chain depth and introduces significant instantiation overhead compared to functional middleware method interception.
  When valid: Viable in architectures where schemas are instantiated via strict object-oriented hierarchies rather than functional compositions.

## Risks

- Behavioral drift between the compiled fast path and the fallback baseline parsing path.
  Mitigation: Implement comprehensive test suites comparing output parity between compiled execution paths and baseline parsing paths.
  Owner: Core Engineering Team
- Unintended property collision or prototype pollution during dynamic error tree assembly.
  Mitigation: Enforce explicit prototype property checks and defensive property definition routines within internal navigation utilities.
  Owner: Core Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Ensure that fast-path compiled execution returns a designated sentinel value to trigger immediate delegation to original methods without throwing unhandled exceptions.
- Maintain strict parity in return signatures between intercepted methods and their fallback implementations across both synchronous and structured execution modes.

## Continuation Context


Verify commands:
- Discover and execute the project validation test suite to confirm parity between compiled fast paths and baseline parsing implementations.
- Discover and execute the project static analysis and linting scripts to verify compliance with internal boundary interception conventions.

Accept when:
- All core parsing and schema validation tests execute and pass when compiled method middleware is engaged.
- Fallback validation behavior executes identically to the uncompiled base implementation whenever the compiled parser returns an invalid sentinel.
- Dynamic property assignments in tree-traversal helpers do not alter or pollute prototype structures.

## Enforcement

- Verified by: Automated test suites validating compiled parsing parity against baseline parsing execution.
- Verified by: Static analysis and architectural review verifying that schema method wrapping adheres to established delegation middleware patterns.
- Violation handling: Pull requests that bypass method interception wrappers in favor of direct destructive mutation are blocked.
- Violation handling: Build pipeline failures on regression test suites that detect divergence between compiled output and baseline parser output.
- Exception process: Propose an architectural amendment demonstrating that the schema execution path cannot be modeled through functional method interception.
- Exception process: Obtain approval from the core engine maintainers before introducing alternative execution hooks.