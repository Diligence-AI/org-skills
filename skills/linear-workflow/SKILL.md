---
name: linear-workflow
description: >-
  Keeps existing Linear work accurate while it moves from Todo through active
  work, review, blockers, and completion. Use when starting or resuming a Linear
  issue, changing its status, posting findings or blockers, or choosing the next
  ready task. Do not use to create a new issue; use create-linear-task instead.
---

# Linear Workflow

Use Linear as the source of truth. Use Linear MCP tools directly, confirm the workspace,
team, and issue before a write, and do not change unrelated issues.

## Keep the issue current

- Put task questions, findings, decisions, and blockers on the issue. Use chat tools only
  for short notifications because issue history must remain easy to find.
- Update status when the real work state changes. Do not rely on daily progress reports to
  correct a stale board.
- Match the team's status category before its display name because workflows differ:
  - Active work or self-review: in progress.
  - Ready but not started, reopened, or changes requested before work resumes: Todo or backlog.
  - Waiting for another reviewer, or for final verification after deployment: in review.
  - Blocked: blocked; if the team has no blocked status, keep it in progress and add a blocker
    comment.
  - Paused before completion: Todo or backlog, based on whether it is ready to resume.
  - Scope complete: completed.
  - Canceled work: canceled, never completed.

When work enters review, add the evidence and the exact remaining check to the issue.

## Do not wait idle

If access, a decision, or another dependency will block useful work for about 30 minutes,
add the blocker to the issue and tag the person who can resolve it. Set the correct blocked
state, then pull the next ready Todo item. When work finishes, pull the next ready item
without waiting for assignment.
