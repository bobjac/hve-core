---
description: "Generate a feature-scoped technical constitution focused on a specific area of the codebase - Brought to you by microsoft/hve-core"
agent: Code With Accelerate
argument-hint: "feature=<feature-spec-url-or-description>"
---

# Generate Feature-Scoped Constitution

## Inputs

- ${input:feature}: (Required) Feature specification URL or description to scope the constitution.

## Requirements

1. Execute Workflow 1: Constitution Generation in feature-scoped mode.
2. Focus research and constitution content on the specific codebase area relevant to `${input:feature}`.
3. Use phased execution (A, B, C) with user confirmation between phases.
4. Produce a targeted constitution covering only the patterns, interfaces, enums, models, and base classes relevant to the specified feature.
5. Run proprietary screening before delivering the final constitution.
6. Output the constitution to `.copilot-tracking/constitution/constitutions/{{YYYY-MM-DD}}/constitution.md`.
