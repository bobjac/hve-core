---
description: "Privacy and security constraints for all CodeWith Accelerate workflows including constitution generation and PoC integration"
applyTo: '**/*'
---

# Privacy and Security Constraints

These constraints apply to all CodeWith Accelerate workflows. They protect customer intellectual property and ensure compliance with Microsoft privacy requirements.

## Constitution Generation Constraints

- MUST NOT include API keys, secrets, or credentials in generated constitutions.
- MUST NOT expose proprietary algorithms or patented processes.
- MUST NOT include internal company names, product codenames, or employee names.
- MUST warn about licensed third-party libraries that require purchase.
- MUST flag any content that appears to contain trade secrets.
- Constitution documents MUST be reviewed by the customer before sharing externally.

## PoC Integration Constraints

- CANNOT access customer source code during PoC development (uses constitution only).
- CANNOT delete customer files without explicit confirmation from the user.
- MUST validate all tests pass after integration changes.
- MUST create backups before making changes to existing files.
- MUST preserve all existing customer code during integration.

## Artifact Security

- All artifacts in `.copilot-tracking/constitution/` contain potentially sensitive information.
- Do not commit `.copilot-tracking/` contents to public repositories.
- Constitution documents should be delivered via secure channels only.
- Integration reports may contain file paths and architecture details that are customer-confidential.

## Tool Usage Restrictions

**Microsoft Employees performing EPS work:**

- MUST use GitHub Copilot for all EPS customer engagement work.
- MUST NOT use Claude Code for EPS work (prevents third-party AI exposure to customer data).

**Customers in their own environments:**

- MAY use any AI coding assistant they choose, including Claude Code or GitHub Copilot.

## Screening Checklist

Before delivering any constitution or integration artifact to a customer, verify:

- [ ] No API keys, secrets, or credentials present
- [ ] No proprietary algorithms or patented processes exposed
- [ ] No internal codenames or employee names included
- [ ] All third-party library licenses documented
- [ ] Customer has reviewed and approved the content
