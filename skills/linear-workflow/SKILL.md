---
name: linear-workflow
description: >-
  Keeps existing Linear work accurate while it moves from Todo through active
  work, review, blockers, and completion, and sets how to write about Linear work
  for a person. Use when starting or resuming a Linear issue, changing its status,
  posting findings or blockers, choosing the next ready task, or writing a
  summary, triage list, plan, or status update about Linear issues for a human
  reader. Do not use to create a new issue; use create-linear-task instead.
---

# Linear Workflow

Use Linear MCP tools directly, confirm the workspace, team, and issue before a write, and do
not change unrelated issues.

## What Linear is for

Linear holds the state of a commitment: what the team agreed to do, who owns it, and where it
stands. It is a ledger, not a workspace and not a document store.

Before any write, ask one question: does this change what someone does next, or who owns it?
If it does not, it does not belong in Linear. Three checks when that is unclear:

- **One breath.** If you can say it in one breath, it is a comment. If it needs a screen
  share, it is a document, and the comment carries the link.
- **Survival.** If the text stops being true when the branch merges, keep it on the branch.
- **The stranger.** In six months, does a person who did not do the work need this to act?

The rest has a better home. How a change was made and reviewed belongs on the pull request.
Why a durable decision was made belongs in a document in the repository. A working note
belongs on the branch, or nowhere.

## Keep the issue current

- A comment is a decision, a pointer, a supplied fact, or a blocker, and it runs to about
  four lines: the decision and its reason; or a branch, pull-request, or document link with
  one line of state; or the client's own words; or what blocks the work and who can clear it.
- Never paste review findings, test counts, root-cause reports, implementation plans, phase
  tables, or long checklists into an issue. Put them where the work is, and link them.
- Write it once. Do not repost the same text on a later visit, and do not send one note to
  many issues. When one change affects a group, say it once on the parent.
- Use chat tools only for short notifications, because issue history must stay easy to find.
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

When work enters review, put the pull-request link on the issue with one line: what it needs,
and the exact remaining check. The evidence itself stays on the pull request.

## Name the work, not the number

An identifier is easy for a tool to read and hard for a person to remember. When you write
to a person about Linear work, say what the issue is in plain words first. Put the
identifier after those words, and only where the reader needs it to open the issue, such as
a handover, a decision list, or a question about one issue. Do not start a sentence, a
bullet, or a table row with a bare identifier. Do not let an identifier replace the
description of the work.

Keep identifiers inside Linear. Issue descriptions, comments, and relations need them.

## Do not wait idle

If access, a decision, or another dependency will block useful work for about 30 minutes,
add the blocker to the issue and tag the person who can resolve it. Set the correct blocked
state, then pull the next ready Todo item. When work finishes, pull the next ready item
without waiting for assignment.
