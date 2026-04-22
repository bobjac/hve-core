---
description: "Securely deliver a generated constitution to an EPS team member via a private GitHub repository - Brought to you by microsoft/hve-core"
agent: Code With Accelerate
argument-hint: "owner=<github-username-or-org> repo=<repo-name> eps=<eps-github-username>"
---

# Deliver Constitution

## Inputs

- ${input:owner}: (Required) GitHub username or organization name where the private repo will be created. Use your personal GitHub username to create the repo under your account, or an organization name to create it under an org.
- ${input:repo}: (Optional) Name for the constitution repository. If not provided, suggest a name based on the project (e.g., `constitution-{{project-name}}`).
- ${input:eps}: (Required) GitHub username(s) of the EPS team member(s) to add as collaborators. Separate multiple usernames with commas.

## Requirements

1. Execute Workflow 1, Phase D: Secure Delivery.
2. Locate the most recent constitution from `.copilot-tracking/constitution/constitutions/`.
3. Create a private GitHub repository under `${input:owner}`.
4. Commit the constitution, README, and LICENSE placeholder to the repo.
5. Add `${input:eps}` as collaborator(s) with write access.
6. Report the repo URL and delivery status.
7. If any step fails (gh not authenticated, org policy blocks creation), provide clear recovery instructions.
