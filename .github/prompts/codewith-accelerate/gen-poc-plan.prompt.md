---
description: "Create an integration plan for a proof-of-concept built from a constitution - Brought to you by microsoft/hve-core"
agent: Code With Accelerate
argument-hint: "poc=<poc-repo-url> [spec=<feature-spec-url>]"
---

# Generate PoC Integration Plan

## Inputs

- ${input:poc}: (Required) PoC repository URL or documentation URL.
- ${input:spec}: (Optional) Feature specification URL for additional context.

## Requirements

1. Execute Workflow 2: PoC Integration, Phase A (Map and Plan) only.
2. Fetch and review PoC documentation from `${input:poc}`.
3. Read the existing constitution document from `.copilot-tracking/constitution/`.
4. Create an integration map documenting:
   - PoC file to customer codebase location mappings
   - Mock service to real service replacement list
   - Interface contract verification results
   - Dependency additions needed
5. Output the integration map to `.copilot-tracking/constitution/integration-reports/{{YYYY-MM-DD}}/integration-map.md`.
6. Present the plan for user review before any code changes.
