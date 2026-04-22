---
description: "Standards for integrating proof-of-concept code into customer codebases following constitution patterns"
applyTo: 'poc-*/**/*.{ts,tsx,cs,js,jsx,py}'
---

# PoC Integration Standards

Apply these standards when integrating proof-of-concept code into a customer codebase.

## Constitution Compliance

- Follow constitution.md patterns exactly for naming conventions, error handling, and logging.
- Extend base classes specified in Section 17 of the constitution.
- Implement interfaces specified in Section 14 of the constitution.
- Use enums specified in Section 15 of the constitution.
- Match model structures from Section 16 of the constitution.

## Integration Safety

- MUST preserve all existing customer code.
- CANNOT delete customer files without explicit confirmation.
- MUST create backups before overwriting existing files.
- MUST validate all tests pass after integration.
- MUST document every file added or modified.

## Mock Service Replacement

When replacing mock services with real implementations:

- Clearly identify each mocked service being replaced.
- Document what real service replaces each mock.
- Verify interface contracts match between mock and real service.
- Update all import statements to reference real implementations.
- Remove mock files only after real service integration is verified.

## Documentation

After integration, create or update `integration-report.md` with:

- All files added to the codebase (with paths).
- All files modified (with paths and change summaries).
- All mock to real service replacements.
- Test results (pass/fail counts).
- Any remaining manual steps for the customer.
