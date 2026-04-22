# Constitution Validation Skill

Validates that generated constitution.md documents meet structural requirements and content minimums for migration-ready quality.

## Validation Checks

- Structure: 18 sections present, correct numbering, Table of Contents
- Content minimums: code examples, interfaces, enums, models, base classes
- Migration-critical completeness: complete contracts in Sections 14-17

## Usage

This skill is invoked by the Code with Accelerate agent after constitution generation and before using a constitution for PoC development. It is not user-invocable.

## Output

A validation report with pass/fail status for each check and specific recommendations for addressing failures.

See [SKILL.md](SKILL.md) for the complete skill specification.

---

<!-- markdownlint-disable MD036 -->
*Crafted with precision by Copilot following brilliant human instruction,
then carefully refined by our team of discerning human reviewers.*
<!-- markdownlint-enable MD036 -->
