---
version: 2
name: 2c27b6d6-c0bf-4784-a35d-536246e6bc2d-zod-schema-declaration-and-runtime-validation-untrusted-external-inputs-integration-payloads-evaluated
description: "Zod Schema Declaration and Runtime Validation: Untrusted External Inputs Integration Payloads Evaluated"
metadata:
  actual:
    adr_id: 2c27b6d6-c0bf-4784-a35d-536246e6bc2d
    status: accepted
    candidate_group_id: e3657d19-8224-4060-91d1-2843c384c02e
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/bench/**
      - packages/integration/fixtures/**
      - packages/resolution/src/**
      - packages/treeshake/**
      - play.ts
---

# Zod Schema Declaration and Runtime Validation: Untrusted External Inputs Integration Payloads Evaluated

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Applies to:
- `packages/bench/**`
- `packages/integration/fixtures/**`
- `packages/resolution/src/**`
- `packages/treeshake/**`
- `play.ts`

## Context

- System boundaries and integration layers receive external and untrusted data payloads requiring strict runtime guarantees.
- Manual parameter assertions and disjoint interface declarations create divergence between static types and dynamic inputs.
- The codebase demonstrates recurring integration of Zod schema definitions across fixtures, benchmarks, resolution modules, and integration surfaces.

## Problem Statement

External and dynamic inputs entering application packages lack runtime safety guarantees when relying solely on static type declarations, leading to potential unhandled malformed payloads and structural type drift across integration layers.

## Decision

1. SHOULD: Untrusted external inputs and integration payloads SHOULD be evaluated using safeParse rather than throwing parse operations to ensure defensive error handling.

## Policy Block

- SHOULD Untrusted external inputs and integration payloads SHOULD be evaluated using safeParse rather than throwing parse operations to ensure defensive error handling.

In scope:
- External data ingestion points, API integration payloads, and boundary contracts across application modules.
- Data model validation logic requiring synchronization between runtime assertions and static typing.

Out of scope:
- Internal closed-loop algorithmic functions operating exclusively on pre-validated data structures.
- Performance-critical micro-benchmarking loops where validation cost dominates execution time and inputs are invariant.

## Rationale

- Zod provides a unified declarative API for building schemas that simultaneously enforce runtime parsing and infer static types.
- Employing a standardized validation library eliminates ad-hoc validation routines and ensures consistent error structures across packages.
- The pattern is substantiated across multiple packages, benchmarks, and integration fixtures within the repository.

## Consequences

Positive:
- Runtime boundary inputs are strictly validated before executing core business logic.
- TypeScript static types and runtime validation rules remain unified through automated schema type inference.
- Validation errors yield structured, actionable diagnostics at the ingestion boundary.

Negative:
- Runtime parsing introduces computational overhead on hot or high-throughput execution paths.
- Bundled client applications incur additional artifact footprint for schema definition and parsing logic.

## Alternatives

- Compile-time type assertions without runtime validation (rejected)
  Rejected because: Pure compile-time types provide zero runtime protection against malformed external inputs or dynamic payloads.
  When valid: Internal closed modules where data sources are guaranteed strictly typed at compile time.
- Ad-hoc manual conditional guards for input checking (rejected)
  Rejected because: Manual conditional checks lack composability, introduce cognitive overhead, and frequently drift from declared type signatures.
  When valid: Extremely constrained micro-runtimes where zero third-party library dependencies can be accommodated.

## Risks

- Validation overhead on high-frequency data ingestion paths may introduce latency bottlenecks.
  Mitigation: Profile critical ingestion pipelines and selectively apply lightweight or pre-compiled schema validation paths where needed.
  Owner: engineering team
- Manual duplication of types alongside schemas could cause synchronization drift.
  Mitigation: Enforce schema type inference as the single source of truth across all domain type definitions.
  Owner: engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Define shared reusable schema primitives in dedicated module boundaries to prevent redundant schema definitions.
- Prefer defensive parsing methods at public ingestion endpoints to capture structured issue reports without triggering uncaught exceptions.

## Continuation Context


Verify commands:
- git grep -E "(safeParse|parse)\(" -- "*.ts" "*.mts" "*.cts"
- find . -name "*test*" -not -path "*/node_modules/*"

Accept when:
- All schema-governed boundary inputs parse incoming payloads using Zod schemas before application processing.
- Verification test suites and type-checking scripts pass without unhandled validation errors or structural drift.

## Enforcement

- Verified by: Automated test suites exercising schema parsing logic and boundary validation.
- Verified by: Static analysis and architectural review of data entry points and external integration layers.
- Violation handling: Pull requests introducing raw unvalidated data casts at external boundaries are blocked during review.
- Violation handling: Failing validation test suites block integration pipelines until schemas or payloads are corrected.
- Exception process: Submit an architecture exception request detailing why runtime schema validation cannot be applied on the targeted boundary.
- Exception process: Obtain sign-off from designated engineering reviewers and document alternative defensive boundary controls.