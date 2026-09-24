# Remark Middleware Processing Pipeline: Engineers Inspect Project Lock Artifact Resolve

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Documentation content containing Markdown, MDX syntax, transcluded file inclusions, and extended formatting requires systematic parsing and transformation before serialization.
- Ad-hoc string manipulation fails to reliably handle nested MDX components, syntax extensions, and transclusions.
- The unified processing ecosystem with remark provides an extensible abstract syntax tree middleware pipeline architecture for chaining syntax plugins.

## Problem Statement

Markdown and MDX documentation content requires structured parsing, extension resolution, and stringification to generate normalized text outputs, but manual string transformations fail to safely handle syntax extensions and transclusions without an abstract syntax tree pipeline.

## Decision

1. MUST: Engineers MUST inspect the project lock artifact and resolve the exact locked version of remark and its associated plugins before implementing pipeline extensions.

## Policy Block

- MUST Engineers MUST inspect the project lock artifact and resolve the exact locked version of remark and its associated plugins before implementing pipeline extensions.

In scope:
- Documentation loaders and transformation pipelines that parse Markdown and MDX documents into serialized text.

Out of scope:
- Static document rendering pipelines handled entirely at build time by framework-native document renderers.
- Non-document data transformations that do not process Markdown or MDX abstract syntax tree structures.

## Rationale

- Chaining middleware via remark use enables composable, modular syntax handling for MDX syntax, transclusion inclusions, and GitHub Flavored Markdown.
- Abstract syntax tree middleware pipelines isolate syntax parsing from stringification, preventing syntax degradation during transformation.
- Standardizing on unified remark middleware avoids redundant custom Markdown parsers across document ingestion components.

## Consequences

Positive:
- Provides modular extensibility where syntax extensions can be added or removed without rewriting parsing logic.
- Ensures reliable handling of MDX structures and file inclusion directives through dedicated abstract syntax tree visitors.
- Enables consistent plain-text and formatted string serialization across documentation ingestion workflows.

Negative:
- Introduces performance overhead associated with full abstract syntax tree construction and traversal.
- Requires maintaining compatibility across multiple independent abstract syntax tree middleware plugins within the pipeline.

## Alternatives

- Regular expression replacement and custom token parsing (rejected)
  Rejected because: Regular expression parsing fails on nested markdown constructs, embedded MDX JSX elements, and multiline transclusions.
  When valid: Trivial single-line text substitutions without structured syntax requirements.
- Framework-integrated build-time compiler components without custom pipeline middleware (rejected)
  Rejected because: Framework build-time compilers do not provide programmatic access to serialized intermediate text for programmatic loaders.
  When valid: Documentation that is only rendered directly to browser viewports without programmatic text extraction.

## Risks

- Mismatches in abstract syntax tree node representations across plugin versions causing pipeline breakage
  Mitigation: Strict lock-file verification and integration testing across chained plugin invocations
  Owner: engineering team
- Processing latency on large documentation trees due to multiple synchronous abstract syntax tree passes
  Mitigation: Profile pipeline execution and cache serialized outputs where content hashes remain unchanged
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
- Construct the remark pipeline by chaining use calls, ensuring input parsers precede intermediate AST transforms and stringify serializers.
- Verify that all plugins registered in the pipeline adhere to the unified syntax tree specification supported by the configured remark version.

## Continuation Context


Verify commands:
- Discover and run the project test runner against documentation loader test suites to verify transformation outputs.
- Discover and execute the project linter and type checker to validate middleware pipeline types and plugin signatures.

Accept when:
- All documentation loader test suites pass, verifying accurate transformation of MDX and Markdown sources into expected serialized strings.
- Static type checks pass with zero errors across all remark pipeline and plugin invocation sites.

## Enforcement

- Verified by: Automated continuous integration pipeline executing unit and integration tests for document loaders.
- Verified by: Architectural and peer code reviews for any modifications to documentation parsing pipelines.
- Violation handling: Pull requests introducing unapproved Markdown parsing mechanisms or unpinned remark plugins are blocked from merging.
- Exception process: Submit an architectural review request outlining technical constraints that necessitate bypassing the remark abstract syntax tree pipeline.