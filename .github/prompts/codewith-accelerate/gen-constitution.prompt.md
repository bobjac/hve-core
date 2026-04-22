---
description: "Generate a full technical constitution for the current codebase - Brought to you by microsoft/hve-core"
agent: Code With Accelerate
argument-hint: "[task description or focus area]"
---

# Generate Constitution

## Inputs

- ${input:task}: (Optional) Additional context or focus area for constitution generation.

## Requirements

1. Execute Workflow 1: Constitution Generation in full mode.
2. Analyze the entire codebase to produce an 18-section constitution document.
3. Use phased execution (A, B, C) with user confirmation between phases.
4. Run proprietary screening before delivering the final constitution.
5. Output the constitution to `.copilot-tracking/constitution/constitutions/{{YYYY-MM-DD}}/constitution.md`.
