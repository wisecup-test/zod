---
version: 2
name: b9c07034-9af4-4ff7-a931-87494628ff02-semver-library-adoption-for-semantic-version-validation-and-comparison-release-validation-routines-handle-invalid-semantic
description: "semver Library Adoption for Semantic Version Validation and Comparison: Release Validation Routines Handle Invalid Semantic"
metadata:
  actual:
    adr_id: b9c07034-9af4-4ff7-a931-87494628ff02
    status: accepted
    candidate_group_id: 88e3c7ec-b2f5-4acc-b756-5dcd64678f07
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# semver Library Adoption for Semantic Version Validation and Comparison: Release Validation Routines Handle Invalid Semantic

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `scripts/**`

## Context

- Release verification routines and package consistency audits require precise parsing and ordering of semantic version identifiers.
- Discrepancies in manual string parsing or regular expression implementations risk misinterpreting pre-release tags, build metadata, or version ranges across distributed packages.
- Standardizing semantic version validation through the semver library guarantees compliance with formal versioning specifications across all automation scripts.

## Problem Statement

Maintaining version alignment and release gating across published packages requires consistent parsing, comparison, and validation of semantic version identifiers. Ad-hoc string splitting or custom comparison algorithms risk inconsistent handling of edge cases such as pre-release identifiers and metadata, leading to undetected lockstep drift or erroneous publication gating.

## Decision

1. SHOULD: Release validation routines SHOULD handle invalid semantic version formats gracefully by logging explicit diagnostic errors before halting execution.

## Policy Block

- SHOULD Release validation routines SHOULD handle invalid semantic version formats gracefully by logging explicit diagnostic errors before halting execution.

In scope:
- Automation scripts, release verification routines, and tooling that parse, compare, or validate package versions.
- Release gating checks that verify version synchronization across multiple published distributions.

Out of scope:
- Runtime application code that does not inspect or compare semantic version numbers.
- Non-versioned identifiers and arbitrary alphanumeric string processing.

## Rationale

- Adopting semver ensures strict adherence to the formal Semantic Versioning specification across all verification workflows.
- Centralizing version parsing in an established library eliminates defect-prone custom version comparison routines.
- Lockstep verification across package distributions requires uniform comparison semantics for pre-release and stable releases.

## Consequences

Positive:
- Deterministic and specification-compliant semantic version parsing and comparison across all verification tooling.
- Elimination of brittle custom regular expressions and ad-hoc string splitting for version comparisons.
- Reliable detection of version drift and lockstep mismatches across distributed packages.

Negative:
- Introduces an external library dependency into the project tooling dependency graph.
- Engineers must ensure the installed library version supports any specific version range syntax required by registry metadata.

## Alternatives

- Custom regular expression parsing and manual string comparison (rejected)
  Rejected because: Regular expressions frequently fail to capture edge cases in semantic versioning specifications such as pre-release precedence and build metadata sorting.
  When valid: Only when operating in constrained environments with zero external dependency allowances and strictly uniform version formats.
- Runtime package manager CLI invocation for version comparison (rejected)
  Rejected because: Spawning external process commands introduces environment coupling, execution latency, and inconsistent behavior across development platforms.
  When valid: When version resolution relies on complex private registry configuration managed exclusively by a specific package manager client.

## Risks

- Incompatibility between the resolved library version and evolving registry version payload formats.
  Mitigation: Lock version grounding mandates inspecting the repository resolution artifact and validating API compatibility before implementation.
  Owner: engineering team
- Failure to catch invalid version inputs causing unhandled exceptions in automated checks.
  Mitigation: Enforce input validation and diagnostic logging around version parsing operations.
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
- Locate the release and version verification modules within the repository to inspect existing patterns for version parsing and error handling.
- Ensure error messages emitted during version validation provide actionable diagnostic context when lockstep discrepancies or format errors occur.

## Continuation Context


Verify commands:
- Discover and execute the project verification script defined in the repository manifest responsible for semver checking.
- Discover and execute the automated lockstep verification script defined in the repository manifest.

Accept when:
- Version validation routines successfully parse and compare version identifiers using the semver library.
- Lockstep verification halts with an error exit code when version mismatches are detected between synchronized packages.
- All automated verification directives pass without unhandled exceptions or syntax errors.

## Enforcement

- Verified by: Automated continuous integration checks executing repository verification scripts.
- Verified by: Peer code review verifying that version comparison routines utilize the adopted library rather than custom logic.
- Violation handling: Pull requests containing custom version parsing or unhandled version discrepancies are blocked from merging.
- Exception process: Exceptions must be documented with an architectural justification and approved by the engineering leads.