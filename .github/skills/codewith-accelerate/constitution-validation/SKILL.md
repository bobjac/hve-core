---
name: constitution-validation
description: 'Validate constitution.md structure, section completeness, and content minimums to ensure migration-ready quality before delivery - Brought to you by microsoft/hve-core'
license: MIT
user-invocable: false
metadata:
  authors: "microsoft/hve-core"
  spec_version: "1.0"
  last_updated: "2026-04-21"
---

# Constitution Validation Skill

This `SKILL.md` is the entrypoint for the constitution validation skill.

The skill validates that a generated constitution.md document meets the required structure, section completeness, and content minimums needed for successful PoC development.

## Purpose

Ensure every generated constitution is migration-ready by validating structural requirements and content minimums. A PoC developer relying on an incomplete constitution will produce code that does not integrate cleanly with the customer's codebase.

## When to Use

- After completing constitution generation (end of Phase C).
- When reviewing an existing constitution for completeness.
- Before using a constitution as input for PoC development.

## Validation Checks

### 1. Structure Validation

| Check | Requirement | Pass Criteria |
|-------|-------------|---------------|
| Section Count | Exactly 18 sections | All 18 sections present with correct numbering |
| Table of Contents | Present at top | TOC exists and links match section headings |
| Section Numbering | Sequential 1-18 | No gaps, no duplicates, correct order |
| Section Headings | Match required titles | Each heading matches the expected section name |

### Required Section Titles

1. Project Overview
2. Technology Stack
3. Architecture Overview
4. Project Structure
5. Coding Standards and Conventions
6. Error Handling Patterns
7. Logging and Observability
8. Configuration Management
9. Authentication and Authorization Patterns
10. Testing Strategy
11. Build and Deployment
12. Code Examples
13. Data Access Patterns
14. Interface Contracts
15. Enum Definitions
16. Model Definitions
17. Base Classes and Inheritance
18. Migration Checklist

### 2. Content Minimum Validation

| Section | Minimum Content | Validation |
|---------|----------------|------------|
| 2. Technology Stack | Version numbers for all dependencies | Check for version patterns (X.Y.Z) |
| 12. Code Examples | 3 runnable examples, 40+ lines each | Count code blocks, measure line counts |
| 14. Interface Contracts | At least 1 interface with complete members | Check for interface definitions with signatures |
| 15. Enum Definitions | At least 1 enum with all values | Check for enum definitions with numeric values |
| 16. Model Definitions | At least 1 model with all properties | Check for model definitions with typed properties |
| 17. Base Classes | At least 1 base class with extension points | Check for base class definitions |

### 3. Migration-Critical Section Validation

Sections 13-17 require deeper validation because PoC developers depend on complete contracts:

**Section 14 (Interface Contracts):**

- Every interface must list all members.
- Each member must include a complete type signature (parameters and return type).
- Generic type parameters must be documented.

**Section 15 (Enum Definitions):**

- Every enum must list all values.
- Each value must include its numeric assignment.
- String enums must include their string values.

**Section 16 (Model Definitions):**

- Every model must list all properties.
- Each property must include its type.
- Required vs. optional must be indicated.
- Nested model references must be resolvable within the document.

**Section 17 (Base Classes):**

- Every base class must list extension points (virtual/abstract members).
- Protected members available to derived classes must be documented.
- Constructor parameters must be listed.

## Output Format

Produce a validation report with the following structure:

```markdown
## Constitution Validation Report

**File:** [path]
**Date:** [YYYY-MM-DD]
**Status:** VALID | WARNINGS | INVALID

### Structure

| Check | Status | Details |
|-------|--------|---------|
| Section Count | PASS/FAIL | Found X of 18 sections |
| Table of Contents | PASS/FAIL | [details] |
| Section Numbering | PASS/FAIL | [details] |

### Content Minimums

| Section | Status | Details |
|---------|--------|---------|
| 12. Code Examples | PASS/FAIL | Found X examples, Y lines average |
| 14. Interfaces | PASS/FAIL | Found X interfaces |
| 15. Enums | PASS/FAIL | Found X enums |
| 16. Models | PASS/FAIL | Found X models |
| 17. Base Classes | PASS/FAIL | Found X base classes |

### Migration-Critical Completeness

| Section | Complete Contracts | Incomplete | Details |
|---------|-------------------|------------|---------|
| 14 | X | Y | [list of incomplete interfaces] |
| 15 | X | Y | [list of incomplete enums] |
| 16 | X | Y | [list of incomplete models] |
| 17 | X | Y | [list of incomplete base classes] |

### Recommendations

- [Specific actions to address validation failures]
```

## Limitations

Content validation relies on pattern matching within markdown. It can verify structural presence and approximate completeness but cannot guarantee semantic correctness. For example, it can confirm that an interface lists members but cannot verify those members match the actual source code.

---

<!-- markdownlint-disable MD036 -->
*Crafted with precision by Copilot following brilliant human instruction,
then carefully refined by our team of discerning human reviewers.*
<!-- markdownlint-enable MD036 -->
