---
name: proprietary-screening
description: 'Scan constitution and integration artifacts for API keys, secrets, proprietary markers, internal codenames, and other sensitive content that must not be shared externally - Brought to you by microsoft/hve-core'
license: MIT
user-invocable: false
metadata:
  authors: "microsoft/hve-core"
  spec_version: "1.0"
  last_updated: "2026-04-21"
---

# Proprietary Screening Skill

This `SKILL.md` is the entrypoint for the proprietary screening skill.

The skill scans constitution documents and integration artifacts for content that must not be shared externally, including secrets, proprietary markers, and internal identifiers.

## Purpose

Detect potential proprietary information in generated constitutions and integration reports before they are delivered to customers or shared across organizational boundaries.

## When to Use

- After completing constitution generation (end of Phase C).
- Before delivering any artifact from `.copilot-tracking/constitution/` to a customer.
- When reviewing integration reports for external sharing.

## Screening Categories

### 1. Secrets and Credentials

Scan for patterns that indicate API keys, secrets, or credentials:

- API key patterns: strings matching `[A-Za-z0-9]{32,}` in configuration contexts
- Connection strings: patterns containing `password=`, `secret=`, `key=`
- Token patterns: `Bearer `, `token:`, `auth:`
- Environment variable references that suggest secrets: `*_KEY`, `*_SECRET`, `*_TOKEN`, `*_PASSWORD`

### 2. Proprietary Algorithm Markers

Scan for language that suggests proprietary or patented content:

- Keywords: "patent", "patented", "proprietary", "trade secret", "confidential"
- Algorithm names that include company-specific prefixes
- References to internal research papers or patents

### 3. Internal Identifiers

Scan for internal company artifacts that should not appear in external documents:

- Internal product codenames (not public-facing names)
- Employee names, aliases, or email addresses
- Internal URLs (intranet, internal wikis, internal dashboards)
- Internal project identifiers or tracking numbers
- Internal team names or organization codes

### 4. Licensed Content

Flag third-party content that may have licensing implications:

- Code snippets from libraries with restrictive licenses (GPL, AGPL)
- Content copied from documentation with copyright notices
- References to commercial libraries that require paid licenses

## Output Format

Produce a screening report with the following structure:

```markdown
## Proprietary Screening Report

**File scanned:** [path]
**Date:** [YYYY-MM-DD]
**Status:** PASS | WARNINGS | FAIL

### Findings

| Category | Severity | Location | Description |
|----------|----------|----------|-------------|
| Secrets  | HIGH     | Line 42  | Possible API key pattern detected |
| Internal | MEDIUM   | Line 108 | Internal URL reference found |

### Recommendations

- [Specific actions to remediate each finding]
```

### Severity Levels

| Severity | Meaning | Action Required |
|----------|---------|-----------------|
| HIGH | Secrets, credentials, or patent references detected | Must remediate before sharing |
| MEDIUM | Internal identifiers or codenames found | Should remediate before sharing |
| LOW | Licensed content or attribution needed | Review before sharing |
| INFO | Potential items flagged for human review | Optional review |

## Limitations

This skill uses pattern-based detection and cannot guarantee complete coverage. It supplements but does not replace human review. All constitutions and integration artifacts must still be reviewed by the customer and appropriate Microsoft personnel before external sharing.

---

<!-- markdownlint-disable MD036 -->
*Crafted with precision by Copilot following brilliant human instruction,
then carefully refined by our team of discerning human reviewers.*
<!-- markdownlint-enable MD036 -->
