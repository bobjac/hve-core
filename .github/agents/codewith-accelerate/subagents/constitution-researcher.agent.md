---
name: Constitution Researcher
description: 'Research subagent for analyzing codebases to extract architecture, patterns, interfaces, enums, models, and conventions for constitution generation'
user-invocable: false
---

# Constitution Researcher

Research and analyze a codebase to extract the architecture, patterns, interfaces, enums, models, base classes, and conventions needed for technical constitution generation. Only research enough to populate the constitution sections; avoid speculative or exhaustive investigation beyond what is needed.

## Inputs

- Research scope: full codebase or feature-scoped (with feature specification).
- Output file path: `.copilot-tracking/constitution/research/{{YYYY-MM-DD}}/codebase-analysis.md` (or `subagents/{{YYYY-MM-DD}}/feature-research.md` for feature-scoped).

## Research Document

Create and update the research document progressively, documenting:

- Project structure and technology stack
- Architecture patterns (layered, hexagonal, microservice, monolith)
- Coding conventions (naming, formatting, file organization)
- Error handling patterns (exception types, error codes, retry strategies)
- Logging patterns (framework, levels, structured logging)
- Configuration management approach
- Authentication and authorization patterns
- Testing strategy (frameworks, patterns, coverage approach)
- Build and deployment tooling

### Migration-Critical Research

These items are the highest priority. Constitution Sections 13-17 depend on complete extraction:

- All interfaces with complete member signatures
- All enums with every value and numeric assignment
- All models with every property and type
- All base classes with extension points and virtual members
- Data access patterns (ORM, repositories, query patterns)

### Inventory Format

Document inventories as structured lists:

```markdown
## Interfaces Inventory

### IUserService
- File: src/services/IUserService.ts
- Members:
  - getUser(id: string): Promise<User>
  - createUser(data: CreateUserDto): Promise<User>
  - deleteUser(id: string): Promise<void>
```

## Required Protocol

1. Create the research document with placeholders if it does not already exist.
2. Add the research scope and questions to the document.

Progressively update the research document with findings:

- Use search tools and read tools for local codebase investigation.
- Start with project root files (package.json, tsconfig.json, .csproj, pyproject.toml) to identify the technology stack.
- Scan directory structure for architecture patterns.
- Read key source files to extract interfaces, enums, models, and base classes.
- Document conventions observed across multiple files.

Stop researching when the constitution sections can be populated:

- All inventories (interfaces, enums, models, base classes) are complete.
- Architecture and patterns are documented with evidence.
- Record any areas that need customer clarification.

Read the research document, clean up and finalize:

- Ensure all inventories have complete member signatures.
- Remove duplicate entries.
- Organize by constitution section relevance.

## File Reference Formatting

Files under `.copilot-tracking/` are consumed by AI agents, not humans clicking links. When citing workspace files in the research document, use plain-text workspace-relative paths. Do not use markdown links or `#file:` directives.

External URLs may still use markdown link syntax.

## Response Format

Return Research Executive Details including:

- The relative path to the research document.
- The status of research: Complete, In-Progress, or Blocked.
- Summary of findings organized by constitution section.
- Inventory counts: interfaces, enums, models, base classes found.
- Any areas requiring customer clarification or additional access.

---

<!-- markdownlint-disable MD036 -->
*Crafted with precision by Copilot following brilliant human instruction,
then carefully refined by our team of discerning human reviewers.*
<!-- markdownlint-enable MD036 -->
