# CodeWith Accelerate: Platform Requirements Document

**Author:** Bob Jacobs
**Date:** 2026-04-28
**Purpose:** Capture the functional and non-functional requirements of the CodeWith Accelerate agent so they can be implemented natively on a new platform.

---

## 1. Executive Summary

CodeWith Accelerate is an orchestrator workflow for **privacy-preserving customer engagements** between Microsoft Enterprise Professional Services (EPS) teams and their customers. It has two primary capabilities:

1. **Constitution Generation** -- Analyze a customer's codebase and produce a comprehensive technical document (called a "constitution") that captures architecture, patterns, interfaces, enums, models, and conventions. The constitution enables EPS teams to build proof-of-concept (PoC) code *without ever accessing the customer's source code*.

2. **PoC Integration** -- Take a proof-of-concept implementation built by EPS (using only the constitution) and integrate it back into the customer's codebase, replacing mocks with real services and adapting to the customer's conventions.

The key privacy invariant is: **EPS never sees customer source code; the customer never has to hand over their repo.** The constitution is the only artifact that crosses the boundary.

---

## 2. Workflow 1: Constitution Generation

### 2.1 Modes

| Mode | Trigger Signals | Scope |
|------|----------------|-------|
| **Full** | "constitution", "generate", "analyze codebase" | Entire codebase |
| **Feature-Scoped** | "feature", "scoped", "spec" + a feature specification URL/description | Only the area of the codebase relevant to the specified feature |

### 2.2 Phase A: Research

**Goal:** Deep analysis of the codebase to gather raw material for the constitution.

**Inputs:**
- The customer's codebase (local workspace)
- Mode (full or feature-scoped)
- Feature specification URL/description (feature-scoped mode only)

**Process:**
1. Analyze project structure and technology stack.
2. Identify architecture patterns and conventions.
3. Extract complete inventories of:
   - Interfaces (all members, full signatures)
   - Enums (all values with numeric assignments)
   - Models (all properties with types)
   - Base classes and inheritance hierarchies (extension points, virtual members)
4. Document error handling patterns, logging patterns, testing strategies.

**Output:** Research document saved to `.copilot-tracking/constitution/research/{date}/codebase-analysis.md`

**Gate:** User must confirm the research summary before proceeding to Phase B.

### 2.3 Phase B: Generate Constitution (Sections 1-12)

**Goal:** Produce the first 12 sections of the constitution from the research output.

**Sections:**

| # | Section | Key Requirements |
|---|---------|-----------------|
| 1 | Project Overview | High-level purpose and scope |
| 2 | Technology Stack | Exact dependency versions |
| 3 | Architecture Overview | Diagrams or descriptions of layers, components |
| 4 | Project Structure | Directory layout and organization rationale |
| 5 | Coding Standards and Conventions | Naming, formatting, patterns in use |
| 6 | Error Handling Patterns | How errors are caught, propagated, reported |
| 7 | Logging and Observability | Frameworks, log levels, structured logging conventions |
| 8 | Configuration Management | How config is loaded, environment handling |
| 9 | Authentication and Authorization Patterns | Auth flows, middleware, token handling |
| 10 | Testing Strategy | Frameworks, conventions, coverage expectations |
| 11 | Build and Deployment | Build tooling, CI/CD, deployment targets |
| 12 | Code Examples | Minimum 3 runnable examples, each 40+ lines |

**Output:** Constitution document saved to `.copilot-tracking/constitution/constitutions/{date}/constitution.md`

**Gate:** User must confirm before proceeding to Phase C.

### 2.4 Phase C: Generate Constitution (Sections 13-18) -- Migration-Critical

**Goal:** Produce the migration-critical sections that are highest priority for PoC development.

**Sections:**

| # | Section | Completeness Requirement |
|---|---------|------------------------|
| 13 | Data Access Patterns | ORM, query patterns, connection management |
| 14 | Interface Contracts | **Every** interface, **all** members, **full** signatures |
| 15 | Enum Definitions | **Every** enum, **all** values with numeric assignments |
| 16 | Model Definitions | **Every** model, **all** properties with types |
| 17 | Base Classes and Inheritance | **All** extension points and virtual members |
| 18 | Migration Checklist | Step-by-step checklist for PoC developers |

**Post-generation steps:**
1. Add a complete Table of Contents with section links at the top of the document.
2. Run proprietary screening (see Section 5.2).
3. Present the completed constitution to the user.
4. Offer secure delivery (Phase D).

### 2.5 Phase D: Secure Delivery (Optional)

**Goal:** Automate the handoff of the constitution to EPS via a private GitHub repository.

**Inputs (collected from user):**
- **GitHub owner** -- username or organization for the repo
- **Repository name** -- suggested default: `constitution-{project-name}`
- **EPS GitHub username(s)** -- collaborators who will receive write access

**Process:**
1. Create a private GitHub repository under the specified owner.
2. Clone to a temporary location.
3. Copy the constitution into the repo.
4. Create a README with usage instructions.
5. Create a LICENSE placeholder (to be replaced by legal).
6. Commit and push.
7. Add each EPS username as a collaborator with write access.
8. Clean up the temporary clone.
9. Report delivery status (repo URL, collaborators added, next steps).

**Error Handling:**

| Error | Recovery |
|-------|----------|
| GitHub CLI not authenticated | Instruct user to run `gh auth login` |
| Repo creation fails (org policy) | Suggest personal account or manual creation |
| Collaborator invitation fails | Suggest manual addition via GitHub settings |
| Constitution file not found | Search `.copilot-tracking/` for most recent constitution |

**Fallback:** If automated delivery fails, provide manual delivery instructions.

---

## 3. Workflow 2: PoC Integration

### 3.1 Required Inputs

- PoC repository URL or documentation URL **(required)**
- Feature specification URL **(optional but recommended)**
- Constitution document path (auto-detected from `.copilot-tracking/constitution/`)

### 3.2 Phase A: Map and Plan

**Goal:** Create a detailed integration plan before any code changes.

**Process:**
1. Fetch and review PoC documentation/code from the provided URL.
2. Read the constitution to understand the customer's patterns.
3. Create an integration map containing:
   - PoC file to customer codebase location mappings
   - Mock services to real service replacement list
   - Interface contract verification (PoC interfaces vs. constitution interfaces)
   - Required dependency additions

**Output:** Integration map saved to `.copilot-tracking/constitution/integration-reports/{date}/integration-map.md`

**Gate:** User must confirm the plan before proceeding to Phase B.

### 3.3 Phase B: Implement Integration

**Goal:** Execute the integration plan.

**Process (per mapped file):**
1. Copy PoC code into the customer codebase at the mapped location.
2. Update code to match customer conventions (naming, error handling, logging, imports).
3. Replace mock services with real service implementations.
4. Update dependency files (package.json, .csproj, requirements.txt, etc.).
5. Follow constitution patterns exactly.

**Safety constraints:**
- NEVER delete customer files without explicit confirmation.
- Preserve all existing customer code.
- Create backups before modifying existing files.

**Gate:** User must confirm changes before proceeding to Phase C.

### 3.4 Phase C: Validate and Report

**Goal:** Verify the integration is correct and complete.

**Process:**
1. Run the full test suite to verify no regressions.
2. Verify all mock services were replaced with real implementations.
3. Verify all interface contracts match between PoC and customer code.
4. Generate a final integration report.

**Output:** Integration report saved to `.copilot-tracking/constitution/integration-reports/{date}/integration-report.md`

**Report contents:**
- Files added and modified (with paths)
- Mock-to-real service replacements performed
- Test pass/fail counts with failure details
- Remaining manual steps (if any)

---

## 4. Artifact Storage

All workflow state and output artifacts are persisted under `.copilot-tracking/constitution/` at the workspace root:

```
.copilot-tracking/constitution/
  research/
    {YYYY-MM-DD}/
      codebase-analysis.md
    subagents/
      {YYYY-MM-DD}/
        feature-research.md
  constitutions/
    {YYYY-MM-DD}/
      constitution.md
  delivery/
    {YYYY-MM-DD}/
      delivery-report.md
  integration-reports/
    {YYYY-MM-DD}/
      integration-map.md
      integration-report.md
      test-results.md
```

**Requirements:**
- Artifacts are date-stamped to support multiple engagements.
- The "continue" workflow detects current state by inspecting which artifacts exist and determines the last completed phase.
- All `.copilot-tracking/` files should begin with `<!-- markdownlint-disable-file -->` and be exempt from linter rules.
- File references within artifacts should use plain-text workspace-relative paths (no markdown links).

---

## 5. Security and Privacy Requirements

### 5.1 Privacy Boundary

The foundational privacy model:

- **During constitution generation:** The agent has full access to customer source code. The constitution it produces must be scrubbed of secrets and proprietary content before leaving the customer's environment.
- **During PoC development (by EPS):** The EPS team works **only** from the constitution. They never access the customer's source code repository.
- **During PoC integration:** The agent has access to both the PoC code and the customer codebase to merge them.

### 5.2 Proprietary Screening (Required Before Delivery)

Before any constitution is delivered, it must be scanned for content that must not be shared externally.

**Screening categories:**

| Category | Examples |
|----------|----------|
| Secrets/Credentials | API keys (32+ char patterns), connection strings, tokens, env var references |
| Proprietary Markers | "patent", "patented", "proprietary", "trade secret", algorithm names |
| Internal Identifiers | Product codenames, employee names/emails, internal URLs, project IDs, team names |
| Licensed Content | GPL/AGPL snippets, copyrighted documentation, commercial libraries requiring licenses |

**Severity levels:**

| Level | Action Required |
|-------|----------------|
| HIGH | Must remediate before delivery |
| MEDIUM | Should remediate before delivery |
| LOW | Review recommended |
| INFO | Optional review |

### 5.3 Constitution Validation

Before delivery, the constitution must be validated for completeness:

- All 18 sections present with sequential numbering
- Table of Contents present and accurate
- Minimum 3 code examples of 40+ lines each
- Sections 14-17 (migration-critical) must have complete inventories:
  - Every interface with all members
  - Every enum with all values
  - Every model with all properties
  - Every base class with extension points

**Validation output:** VALID, WARNINGS, or INVALID with specific recommendations.

### 5.4 Tool Restrictions

| User | Allowed Tools | Rationale |
|------|--------------|-----------|
| Microsoft EPS employees | GitHub Copilot only | Prevents third-party AI exposure to customer data |
| Customers | Any AI assistant (Copilot, Claude Code, etc.) | Their own environment, their choice |

### 5.5 Content Prohibitions

Constitutions and integration artifacts must NEVER contain:
- API keys, secrets, or credentials
- Proprietary algorithms or patented processes
- Internal company codenames or employee names
- Internal URLs or project identifiers

---

## 6. User Interaction Model

### 6.1 Intent Detection

The platform must detect user intent from natural language and route to the correct workflow:

| Signal Words | Routed Workflow |
|-------------|----------------|
| "constitution", "generate", "analyze codebase" | Constitution Generation (full mode) |
| "feature", "scoped", "spec" | Constitution Generation (feature-scoped mode) |
| "deliver", "share", "transfer", "send constitution" | Secure Delivery (Phase D only) |
| "integrate", "poc", "proof of concept", "migration" | PoC Integration |
| "continue", "next", "phase" | Resume last in-progress workflow |

When intent is ambiguous, the platform must ask the user to clarify before proceeding.

### 6.2 Phased Execution with Confirmation Gates

Every workflow is broken into phases (A, B, C, optionally D). Between each phase:

1. The platform presents a summary of what was completed.
2. The user must explicitly confirm before the next phase begins.
3. The user may request changes or adjustments before continuing.

This prevents runaway execution and ensures the user maintains control.

### 6.3 Resume / Continue

The platform must support resuming an interrupted workflow:
- Detect the last completed phase by inspecting which artifacts exist in `.copilot-tracking/`.
- The user may optionally specify which phase to resume (e.g., "continue from Phase C").
- Pick up where the workflow left off without re-executing completed phases.

---

## 7. Subagent / Task Decomposition

The orchestrator delegates to two specialized workers:

### 7.1 Constitution Researcher

- **Purpose:** Deep codebase analysis focused on extracting constitution source material.
- **Inputs:** Research scope (full or feature-scoped), output file path.
- **Outputs:** Structured research document with complete inventories.
- **Completion criteria:** Research is complete when all constitution sections can be populated and all interface/enum/model/base-class inventories are exhaustive.

### 7.2 PoC Integrator

- **Purpose:** Execute the mechanical integration of PoC code into the customer codebase.
- **Inputs:** Integration map path, mock replacement list, phase identifier.
- **Outputs:** Modified file list, test results, integration status.
- **Safety:** Never deletes customer files; preserves all existing code; creates backups.

**Orchestration rules:**
- Only the orchestrator manages subagent calls (subagents do not spawn their own subagents).
- Subagents may run in parallel when their work has no dependencies.

---

## 8. Non-Functional Requirements

| Requirement | Detail |
|------------|--------|
| **Phased output** | Workflows are split into phases to manage response size and enable incremental review |
| **Idempotent resume** | Resuming a workflow must not duplicate or corrupt previously generated artifacts |
| **Date-stamped artifacts** | All outputs are date-stamped to support multiple engagements over time |
| **Graceful degradation** | If GitHub CLI is unavailable, delivery falls back to manual instructions |
| **Linter compatibility** | Generated artifacts include markdownlint-disable directives |
| **No interactive prompts in scripts** | All automation must run non-interactively |

---

## 9. Summary of Platform Capabilities Needed

To natively implement the CodeWith Accelerate workflow, the platform needs:

1. **Codebase analysis engine** -- Ability to deeply analyze a codebase and extract structure, patterns, interfaces, enums, models, base classes, and conventions.
2. **Structured document generation** -- Produce a well-structured 18-section markdown constitution with completeness validation.
3. **Proprietary screening** -- Scan generated documents for secrets, proprietary content, internal identifiers, and licensing issues before delivery.
4. **Phased workflow engine** -- Support multi-phase workflows with user confirmation gates between phases and the ability to resume from any phase.
5. **Intent detection / routing** -- Detect user intent from natural language and route to the appropriate workflow or phase.
6. **GitHub integration** -- Create private repos, add collaborators, commit and push files via the GitHub API.
7. **PoC integration engine** -- Map PoC code to customer codebase locations, replace mocks with real services, adapt conventions, and validate via test suite execution.
8. **Artifact persistence** -- Date-stamped storage for research, constitutions, delivery reports, and integration reports.
9. **Task decomposition** -- Ability to delegate specialized work (research, integration) to focused sub-tasks that can run in parallel.
10. **Privacy enforcement** -- Enforce the boundary that EPS never accesses customer source code and that constitutions are screened before delivery.
