---
version: 2
name: 2690918f-f47c-4e81-b216-cfc8b8201da3-node-fs-promises-metadata-deserialization-when-consuming-versioned-runtime-library-dependencies
description: "node:fs/promises Metadata Deserialization: When Consuming Versioned Runtime Library Dependencies"
metadata:
  actual:
    adr_id: 2690918f-f47c-4e81-b216-cfc8b8201da3
    status: accepted
    candidate_group_id: 11e6ee2f-8e4e-497b-bec8-a88de0f821d5
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/llms-full.txt/**
---

# node:fs/promises Metadata Deserialization: When Consuming Versioned Runtime Library Dependencies

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `app/llms-full.txt/**`

## Context

- Local documentation assets and metadata manifests reside on the local filesystem and require asynchronous retrieval during server-side route generation.
- The documentation endpoint consumes internal loaders and asynchronous filesystem routines from node:fs/promises to load file contents into memory.
- Direct deserialization via JSON.parse is used to decode stringified metadata without external validation overhead.
- The single-point usage in documentation routes presents a lightweight footprint but lacks structured defense against malformed local payloads.

## Problem Statement

Server route handlers reading local filesystem resources require reliable asynchronous ingestion and parsing of metadata. While standard language built-ins and runtime modules offer zero-dependency execution, unvalidated deserialization risks runtime crashes if local files contain malformed syntax or unexpected property structures.

## Decision

1. MUST: When consuming versioned runtime or library dependencies for parsing and file operations, developers MUST inspect the repository dependency manifest and lock artifact to resolve the exact version before implementation.

## Policy Block

- MUST When consuming versioned runtime or library dependencies for parsing and file operations, developers MUST inspect the repository dependency manifest and lock artifact to resolve the exact version before implementation.

In scope:
- Server route handlers and endpoint loaders performing asynchronous reads of local filesystem metadata.
- Internal metadata processing workflows using runtime filesystem modules.

Out of scope:
- Client-side components without access to runtime filesystem modules.
- External network requests governed by perimeter security gateways and HTTP payload validators.

## Rationale

- Utilizing node:fs/promises provides non-blocking asynchronous file operations native to the runtime environment without introducing third-party filesystem wrappers.
- Direct JSON.parse execution offers minimal execution overhead for trusted local metadata files generated during internal build steps.
- Restricting pattern scope to internal documentation route handlers confines parsing risks away from public ingestion endpoints.

## Consequences

Positive:
- Eliminates external dependency bloat by relying on standard runtime filesystem capabilities.
- Provides asynchronous non-blocking I/O during server route execution.
- Keeps metadata ingestion logic simple and co-located with documentation route handlers.

Negative:
- Direct JSON.parse calls lack type guards or runtime schema enforcement, propagating structural errors downstream.
- Malformed metadata on disk leads to immediate unhandled exceptions unless explicitly caught in the handler.
- Pattern is localized to a single file, lacking architectural uniformity across the broader codebase.

## Alternatives

- Adopt a dedicated schema validation library for all local filesystem metadata parsing (deferred)
  Rejected because: Adding an external validation dependency introduces unnecessary bundle and maintenance overhead for single-file static documentation metadata.
  When valid: When metadata schemas become complex or originate from untrusted external user input.
- Synchronous filesystem reads using blocking runtime APIs (rejected)
  Rejected because: Synchronous file operations block the runtime event loop during server route handling, reducing request throughput.
  When valid: During initial application startup before accepting network requests.

## Risks

- Syntax errors in local metadata files cause JSON.parse to throw unhandled runtime exceptions.
  Mitigation: Wrap deserialization calls in error handling blocks and log descriptive error diagnostics.
  Owner: Engineering Team
- Schema drift between stored metadata files and internal loaders causing missing properties.
  Mitigation: Add unit tests that validate metadata structure against expected loader types during build verification.
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
- Isolate filesystem reads to asynchronous functions to avoid event loop stalls during route resolution.
- Implement defensive error handling around JSON.parse invocations to gracefully handle unexpected file formats.

## Continuation Context


Verify commands:
- Discover the project script runner and execute the automated test suite targeting route handlers and metadata loaders.
- Discover the static analysis and linting command from the repository manifest and execute it against secure coding rules.
- Inspect the build definition scripts and run the compilation check to confirm type safety across route handlers.

Accept when:
- Automated tests covering metadata retrieval and parsing pass without unhandled rejection or syntax errors.
- Static verification scripts report zero violations regarding unvalidated deserialization.
- Route execution successfully completes metadata ingestion and document ordering without throwing unhandled exceptions.

## Enforcement

- Verified by: Automated test execution verifying route handling and metadata parsing resilience.
- Verified by: Pull request code reviews ensuring proper error boundaries around asynchronous filesystem reads.
- Violation handling: Pull requests omitting error boundaries or introducing synchronous filesystem calls must be blocked until remediated.
- Exception process: Exceptions must be documented in code review and approved by the engineering lead when parsing non-JSON assets.