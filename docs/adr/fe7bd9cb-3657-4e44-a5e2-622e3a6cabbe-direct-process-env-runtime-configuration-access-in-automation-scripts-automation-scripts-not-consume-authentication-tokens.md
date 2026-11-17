---
version: 2
name: fe7bd9cb-3657-4e44-a5e2-622e3a6cabbe-direct-process-env-runtime-configuration-access-in-automation-scripts-automation-scripts-not-consume-authentication-tokens
description: "Direct process.env Runtime Configuration Access in Automation Scripts: Automation Scripts Not Consume Authentication Tokens"
metadata:
  actual:
    adr_id: fe7bd9cb-3657-4e44-a5e2-622e3a6cabbe
    status: accepted
    candidate_group_id: 2cca4728-a9b2-4bc1-8b4e-e02788c4b31b
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Direct process.env Runtime Configuration Access in Automation Scripts: Automation Scripts Not Consume Authentication Tokens

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `scripts/**`

## Context

- Repository automation and maintenance scripts require runtime configuration parameters to control test fuzzing depth, package publication metadata, and automated continuous integration pipeline outputs.
- Script implementations directly read execution environment variables through the runtime process.env global property rather than introducing external secrets management or configuration abstraction libraries.
- The values extracted from process.env encompass iteration limits, tag specifications, package identifiers, and workflow output destination paths, representing non-sensitive operational parameters rather than credentials or encryption keys.

## Problem Statement

Repository automation scripts require runtime parameters to modulate execution depth, package metadata checks, and continuous integration pipeline signaling. Relying on direct global process.env access provides minimal overhead for non-sensitive automation switches, but lacks schema-level sanitization, credential protection, or formal secret boundary isolation.

## Decision

1. MUST_NOT: Automation scripts MUST NOT consume authentication tokens, private keys, or sensitive credentials directly via plain-text process.env references without dedicated credential masking or secret management isolation.

## Policy Block

- MUST_NOT Automation scripts MUST NOT consume authentication tokens, private keys, or sensitive credentials directly via plain-text process.env references without dedicated credential masking or secret management isolation.

In scope:
- Repository automation, validation, and maintenance scripts reading execution parameters and pipeline signaling variables.

Out of scope:
- Production application runtime modules, public library export surfaces, and authentication or credential-handling subsystems.

## Rationale

- Observed script implementations across the repository access execution switches such as iteration bounds, tag identifiers, and pipeline output files directly via runtime process.env without external configuration dependencies.
- Direct runtime process.env access introduces zero external dependency footprint for lightweight repository automation tasks while maintaining transparency across execution environments.
- The accessed variables represent operational switches rather than confidential secrets, warranting lightweight environment access while preserving clear separation from credential handling infrastructure.

## Consequences

Positive:
- Zero external dependency footprint and no initialization overhead for lightweight repository maintenance and testing routines.
- Native compatibility with continuous integration workflows and standard execution environments without configuration loader boilerplate.
- Explicit property-based access clearly documents runtime configuration dependencies directly in script code.

Negative:
- Absence of automated schema parsing or type coercion requires manual type parsing for non-string values.
- No built-in secret masking or audit logging if sensitive credentials are inadvertently passed through standard environment variables.
- Runtime failures can occur silently if expected environment variables are undefined and lack explicit default fallbacks.

## Alternatives

- Adopting a dedicated third-party configuration or secret management library across all repository automation scripts (rejected)
  Rejected because: Introduces unnecessary external runtime dependencies and setup complexity for simple automation scripts that only consume non-sensitive execution flags
  When valid: When application components require structured secret rotation, encryption at rest, or multi-source environment hierarchy loading
- Hardcoding execution switches and pipeline parameters directly within script source files (rejected)
  Rejected because: Eliminates runtime flexibility and prevents continuous integration pipelines from modulating execution parameters without source code changes
  When valid: When values are universally invariant across all local and continuous integration execution environments

## Risks

- Accidental exposure of sensitive credentials if environment variables containing secrets are logged or referenced in automation scripts
  Mitigation: Enforce strict isolation between operational execution flags and secrets, and avoid dumping environment dictionaries to logging streams
  Owner: engineering team
- Runtime execution errors or NaN values resulting from unparsed or missing environment variable strings
  Mitigation: Implement defensive presence checks and explicit string-to-number validation with fallback defaults
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
- Discover repository script definitions through the project configuration manifest and verify environment variable requirements prior to script execution.
- Ensure all environment variable access points define clear fallback default values when variables are omitted in local development environments.

## Continuation Context


Verify commands:
- Discover and run the project repository script verification and type-checking suites across automation scripts.
- Execute the repository linting and static analysis suite to check for unvalidated environment variable references.

Accept when:
- All automation and maintenance scripts execute cleanly without unhandled undefined environment variable exceptions.
- Static analysis and type checking pass across all repository automation scripts without unhandled configuration types.

## Enforcement

- Verified by: Automated continuous integration pipeline execution across pull requests.
- Verified by: Peer code review verification of script modifications and environment variable usage.
- Violation handling: Pull requests introducing unvalidated or sensitive credential handling via plain environment variables are blocked until remediated.
- Exception process: Exceptions require documented review and architectural sign-off justifying why direct environment access is insufficient or why dedicated secret retrieval is needed.