---
version: 2
name: 3ba1b379-854d-4fc1-8480-6a95c3aa3bbb-node-fs-module-adoption-for-filesystem-operations-when-interacting-versioned-modules-repository-dependencies
description: "node:fs Module Adoption for Filesystem Operations: When Interacting Versioned Modules Repository Dependencies"
metadata:
  actual:
    adr_id: 3ba1b379-854d-4fc1-8480-6a95c3aa3bbb
    status: accepted
    candidate_group_id: 94b4be7d-f692-465c-af7a-c152e660ebb3
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/tsc/**
      - scripts/**
---

# node:fs Module Adoption for Filesystem Operations: When Interacting Versioned Modules Repository Dependencies

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `packages/tsc/**`
- `scripts/**`

## Context

- Repository tooling and code generation workflows require direct access to host filesystem resources to read configuration manifests and emit package artifacts.
- Import specifiers without explicit namespace qualifiers risk ambiguous resolution between platform core modules and potential third-party registry packages.
- Synchronous filesystem operations provide deterministic execution order in short-lived automation scripts where asynchronous scheduling adds unnecessary coordination overhead.

## Problem Statement

Repository maintenance scripts and package generation utilities require dependable filesystem access to inspect metadata and generate workspace outputs. Without a standardized import convention and execution model, filesystem interactions risk module resolution shadowing, inconsistent error propagation, and unpredictable timing in build automation.

## Decision

1. MUST: When interacting with versioned modules or repository dependencies, the consumer MUST inspect the repository lock artifact to determine the authoritative resolved version before invoking version-dependent logic.

## Policy Block

- MUST When interacting with versioned modules or repository dependencies, the consumer MUST inspect the repository lock artifact to determine the authoritative resolved version before invoking version-dependent logic.

In scope:
- Repository automation scripts, code generators, and verification routines requiring direct host filesystem access
- Build-time manifest inspection and artifact generation workflows

Out of scope:
- Runtime client packages distributed for cross-platform execution that do not operate in host filesystem environments
- Asynchronous streaming I/O workflows that require non-blocking event-driven pipelines

## Rationale

- Adopting the explicit node:fs protocol specifier guarantees unambiguous module resolution by enforcing core runtime loading and preventing shadowing by registry dependencies.
- Employing readFileSync aligns with the execution model of linear build scripts, eliminating asynchronous orchestration complexity while preserving deterministic execution order.
- Evidence across multiple script and package modules demonstrates consistent reliance on explicit protocol imports and synchronous file parsing.

## Consequences

Positive:
- Eliminates potential module resolution collisions between platform core capabilities and external dependencies.
- Simplifies script flow by avoiding promise resolution chains and asynchronous boilerplate in linear execution tasks.
- Ensures consistent file reading and parsing patterns across all repository maintenance utilities.

Negative:
- Synchronous I/O blocks the process execution thread during file read operations.
- Limits applicability to CLI and build-time environments, preventing reuse within non-blocking runtime services.

## Alternatives

- Un-prefixed core filesystem module specifiers (rejected)
  Rejected because: Leaves module resolution vulnerable to namespace shadowing from registry packages and lacks explicit namespace qualification
  When valid: Legacy execution environments that lack support for protocol-qualified module namespaces
- Asynchronous promise-based filesystem APIs (rejected)
  Rejected because: Introduces unnecessary event loop scheduling and asynchronous orchestration complexity into linear build scripts
  When valid: High-throughput server runtimes handling concurrent non-blocking I/O operations

## Risks

- Synchronous file operations block process execution when reading exceptionally large files
  Mitigation: Restrict synchronous operations to small manifest inspection and deterministic generation artifacts
  Owner: Engineering Team
- Uncaught exceptions during file reading or JSON parsing terminate script execution abruptly
  Mitigation: Encapsulate read and parse operations within structured error handling blocks that provide actionable diagnostics
  Owner: Engineering Team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Import node:fs using protocol-prefixed specifiers across all tooling and generation modules to ensure unambiguous runtime resolution.
- Invoke readFileSync with explicit character encoding parameters when loading repository manifests to prevent buffer decoding anomalies.

## Continuation Context


Verify commands:
- Discover and execute the repository verification script that checks manifest integrity.
- Discover and run the build generation pipeline to confirm all generated artifacts match the declared schema.

Accept when:
- All build scripts and code generators import filesystem capabilities through the explicit node:fs protocol specifier without resolution errors.
- Manifest inspection workflows successfully load and parse target configuration files synchronously without unhandled exceptions.

## Enforcement

- Verified by: Automated static analysis and linting rules in the continuous integration pipeline
- Verified by: Code review validation for changes to repository build and verification scripts
- Violation handling: Continuous integration checks will fail on un-prefixed core module imports or asynchronous operations in synchronous script paths
- Violation handling: Pull requests containing violations will be blocked from merging until corrected
- Exception process: Submit an architectural review request documenting why an un-prefixed module or alternative filesystem strategy is strictly necessary.