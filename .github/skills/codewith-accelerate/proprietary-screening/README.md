# Proprietary Screening Skill

Scans constitution documents and integration artifacts for content that must not be shared externally.

## Screening Categories

- Secrets and credentials (API keys, connection strings, tokens)
- Proprietary algorithm markers (patents, trade secrets)
- Internal identifiers (codenames, employee names, internal URLs)
- Licensed content (restrictive licenses, commercial dependencies)

## Usage

This skill is invoked by the Code with Accelerate agent after constitution generation (Phase C) and before delivering artifacts externally. It is not user-invocable.

## Output

A screening report with findings categorized by severity (HIGH, MEDIUM, LOW, INFO) and specific remediation recommendations.

See [SKILL.md](SKILL.md) for the complete skill specification.

---

<!-- markdownlint-disable MD036 -->
*Crafted with precision by Copilot following brilliant human instruction,
then carefully refined by our team of discerning human reviewers.*
<!-- markdownlint-enable MD036 -->
