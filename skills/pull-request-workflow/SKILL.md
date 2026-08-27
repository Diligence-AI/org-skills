---
name: pull-request-workflow
description: >-
  Runs the Diligence AI branch, pull-request, self-review, QA, human-review, and
  merge workflow. Use when creating a work branch or PR, preparing a PR for
  review, responding to review changes, deciding merge readiness, or merging.
  Do not use for a read-only review that will not change PR state.
---

# Pull Request Workflow

Confirm `gh auth status`, then use authenticated `gh` directly for GitHub operations. For
GitLab, use its configured authenticated tooling. Existing repository permissions and the
operator's task authority remain the limit.

1. Branch from `dev` or the repository default. Keep code and its task documentation on one
   branch, and link the plan or task document from the Linear issue when one exists.
2. Open a draft PR as soon as the branch has a change that GitHub or GitLab can compare. Link
   the PR from its Linear issue when the task is tracked there.
3. Share the PR link, not a raw file or commit link.
4. Before asking for human review, run a thorough self-review in fresh agent context. Resolve
   each valid finding, then test the change end to end in the way a user will use it.
5. Write a PR description that explains what changed, why, how it was tested, and what needs
   reviewer attention. State any deliberate omission and link its tracking issue.
6. Mark the PR ready only after self-review and QA pass. Every PR needs final human review.
7. Any code change after the review gate repeats the gate: self-review, QA, and human
   approval must pass again before merge.
8. Merge only with the required approval, passing required checks, and explicit authority for
   the merge. Do not bypass repository controls.

For an operator-requested Opus or Fable review, use
[external-code-review](../external-code-review/SKILL.md). For user-flow testing after a
feature reaches staging, use [staging-browser-qa](../staging-browser-qa/SKILL.md).

For the Diligence org-skills repository, follow
[org-skill-authoring](../org-skill-authoring/SKILL.md); its ready-PR rule overrides the
draft-PR rule above.
