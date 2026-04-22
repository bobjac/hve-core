---
description: "Continue the current phased execution in a constitution generation or PoC integration workflow - Brought to you by microsoft/hve-core"
agent: Code With Accelerate
argument-hint: "[phase=A|B|C]"
---

# Continue

## Inputs

- ${input:phase}: (Optional) Specific phase to continue with. When absent, resume from the last completed phase.

## Requirements

1. Detect the current workflow state from `.copilot-tracking/constitution/` artifacts.
2. Determine which phase was last completed.
3. Proceed to the next phase in sequence (A, B, C).
4. If `${input:phase}` is specified, jump to that phase directly.
5. Follow the same phased execution protocol with user confirmation at phase boundaries.
