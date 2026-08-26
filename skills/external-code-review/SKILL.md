---
name: external-code-review
description: >-
  Runs an independent, read-only code review with the Claude Code CLI. Use when
  the operator says "review with Claude", "Claude review", "review with Opus",
  or "review with Fable". Selects the exact requested model and lets the paid
  review finish. Do not use for a normal review by the current coding agent.
---

# External Code Review

Run one fresh Claude Code review from the repository or issue worktree that contains the
change.

## Review workflow

1. Read the repository instructions. Identify the full review target and its correct base
   branch. Include committed and uncommitted work that is in scope.
2. Select the model exactly:
   - "Opus" means `--model opus`.
   - "Fable" means `--model fable`.
   - If no model is named, omit `--model` and use the configured Claude default.
   - Do not replace an explicit model with another model.
3. Start a new non-interactive, read-only session. Use `--permission-mode plan` and
   `--no-session-persistence`. Do not resume an earlier session because fresh context is
   the purpose of this review.
4. Give Claude this review brief, with the target and base filled in:

   ```text
   Act as an independent code reviewer. Review the complete <target> against <base>.
   Read the repository instructions first. Do not edit files or create commits.

   Find concrete correctness defects, regressions, security risks, data-loss risks,
   compatibility problems, and missing tests. Do not report style preferences unless
   they cause a defect. Put findings first and order them by severity. For each finding,
   give a P0-P3 priority, exact file and line, failure scenario, reason, and smallest safe
   fix. If there are no findings, say so and list residual test risks.
   ```

5. Let the command finish. A quiet process can still be working. Check its process state
   and continue to wait. Do not stop or restart a healthy review, because that wastes the
   paid run. Do not set `--max-budget-usd` unless the operator gives a limit. Retry only
   after the command exits without a usable result.
6. Check each finding against the source and tests. Do not present a finding as valid
   without evidence. Make changes only when the operator also asked for fixes.
7. Report the model, review target, command completion, accepted findings, rejected
   findings, and tests run after any fixes.

Use the same flags for each model:

```bash
claude -p --model opus --permission-mode plan --no-session-persistence <<'REVIEW'
<review brief>
REVIEW

claude -p --model fable --permission-mode plan --no-session-persistence <<'REVIEW'
<review brief>
REVIEW
```

Never put secrets, credentials, or `.env` content in the prompt.
