---
name: task-execution
description: >-
  Guides Diligence AI execution choices for planning, reversible implementation,
  decision requests, delegating a task to Codex with a chosen model, and staying
  productive while blocked. Use when deciding whether to plan first, build a thin
  slice, ask the operator, or switch tasks, and when starting a Codex task or
  picking the model it runs on. Do not use as the PR review or Linear status
  procedure.
---

# Task Execution

Match the process to the cost of a wrong decision.

- For reversible, low-stakes work, build a small working version and show it. A concrete
  result gives better feedback than a long plan.
- Plan before large work with many moving parts or changes that are difficult to undo.
- Use the installed `grilling` skill when a plan needs a fresh pressure test before it is
  shared.
- Ask for a decision when product scope, a hard-to-reverse migration, a public API, a
  client-facing commitment, or a choice that blocks teammates is unresolved. Do not infer
  approval for these actions.
- Make a decision request easy to answer: use one to three high-level bullets, give a
  recommendation, and state the main tradeoff.
- Use Context7 when the work depends on current library, framework, SDK, API, CLI, or cloud
  service documentation.
- While waiting for an answer, move to other ready work that does not depend on it.

## Delegating to Codex

`codex-start-task` takes no model argument. It uses the default in `~/.codex/config.toml`,
which is often not the model the task calls for. Check it before dispatching:
`grep -m1 '^model' ~/.codex/config.toml`.

- `codex exec -m <model> "<request>"` pins the model for one task and changes no config.
  That run is not resumable from the desktop app, so give the full brief up front and say so
  in the handoff.
- Changing the default in `~/.codex/config.toml` keeps tasks resumable through the managed
  daemon, but it affects every later session. Ask the operator before editing it.
- When the required model is unavailable either way, report the limit. Do not substitute
  another model without saying so.
- Name the model that ran in the handoff, so the operator can see which one did the work.
