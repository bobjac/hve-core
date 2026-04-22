---
description: "Integrate a proof-of-concept implementation into the customer codebase - Brought to you by microsoft/hve-core"
agent: Code With Accelerate
argument-hint: "poc=<poc-repo-url> [spec=<feature-spec-url>]"
---

# Integrate PoC

## Inputs

- ${input:poc}: (Required) PoC repository URL or documentation URL.
- ${input:spec}: (Optional) Feature specification URL for additional context.

## Requirements

1. Execute the full Workflow 2: PoC Integration (all phases A, B, C).
2. Phase A: create integration map from PoC documentation and constitution.
3. Phase B: delegate implementation to `PoC Integrator` subagent.
4. Phase C: validate tests pass and generate integration report.
5. Use phased execution with user confirmation between phases.
6. Output integration report to `.copilot-tracking/constitution/integration-reports/{{YYYY-MM-DD}}/integration-report.md`.
