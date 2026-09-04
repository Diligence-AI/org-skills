---
name: how-we-work
description: >-
  Routes Diligence AI work to focused org skills for Linear workflow, task
  execution, pull-request delivery, client communication, changelogs, org-skill
  authoring, or the grilling and wayfinder working modes. Use at the start of a task,
  when blocked, or when unsure which team workflow applies. This is the lightweight
  index, not each full procedure.
---

# How We Work

Use this skill as an index. Read only the linked skill needed for the current action;
do not load every workflow by default.

## Work tracking

- Starting, resuming, updating, blocking, or completing work tied to Linear: read
  [linear-workflow](../linear-workflow/SKILL.md).
- Creating a new Linear issue: read
  [create-linear-task](../create-linear-task/SKILL.md).

## Working modes

Companion skills from [Matt Pocock's library](https://github.com/mattpocock/skills), not org
skills. Install them separately (see the org-skills README). When they are installed as the
Claude Code plugin, prefix each name with `mattpocock-skills:`.

- Pressure-testing a plan, design, or scope before building: run `/grill-with-docs` inside a
  repository, or `/grill-me` when there is no working directory. The docs variant writes each
  agreed term to `CONTEXT.md` and each hard-to-reverse decision to an ADR, so the next session
  reads the vocabulary instead of re-deriving it.
- Planning an effort too large for one session, where the route to the goal is not yet visible:
  run `/wayfinder`. It charts decision tickets on the issue tracker and resolves one per
  session. It produces decisions, not code, so hand off to the delivery skills below once the
  route is clear. It reads `docs/agents/issue-tracker.md`, so run
  `/setup-matt-pocock-skills` once per repository first and point it at Linear; without that
  file wayfinder stops and asks for it.

Reach for a working mode before the delivery skills, not instead of them.

## Delivery

- Deciding whether to plan, build, ask for a decision, or move to other work: read
  [task-execution](../task-execution/SKILL.md).
- Creating a branch or PR, reviewing, testing, marking ready, or merging: read
  [pull-request-workflow](../pull-request-workflow/SKILL.md).
- Running an independent Claude review: read
  [external-code-review](../external-code-review/SKILL.md).
- Verifying a completed feature in staging: read
  [staging-browser-qa](../staging-browser-qa/SKILL.md).

## Client communication

- Drafting a client message, status update, blocker, or recommendation: read
  [client-communication](../client-communication/SKILL.md).
- Writing a client changelog entry, release note, or short fix summary: read
  [client-changelog](../client-changelog/SKILL.md).

## Skill maintenance

- Creating or updating a Diligence org skill: read
  [org-skill-authoring](../org-skill-authoring/SKILL.md).
- Authoring, reviewing, or debugging any `SKILL.md`: read
  [writing-skills](../writing-skills/SKILL.md).

If one task spans more than one category, read each relevant skill when that part of the
work starts.

## Shared tool boundary

Use Linear MCP tools directly for Linear work and authenticated `gh` directly for GitHub
work. Use the configured authenticated GitLab tooling for a GitLab repository. Use Context7
for current library and framework documentation. Do not route these operations through a
generic wrapper CLI or task proxy. Existing account, team, repository, and task authority
remain the limit.

> **Board is truth · Act on reversible work · Surface blockers fast · Verify before review ·
> Communicate plainly.**
