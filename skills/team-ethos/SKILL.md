---

name: team-ethos
description: >-
  Diligence AI team operating ethos — how we plan, branch, ship, track work in
  Linear, communicate, and stay unblocked. Consult at the START of any task and
  whenever you are blocked, picking your next task, opening a PR, or drafting a
  message that may reach a client. This is the shared "how we work" manual so no
  one has to keep it in their head.
---

# How We Work — Team Ethos

This is our shared operating manual. Follow it on every task so the working style is
consistent across the team and nobody has to remember it from memory. It is short on
purpose. Six principles.

> **Prerequisite.** This workflow runs on connected MCPs — **Linear** (source of truth),
> **GitHub/GitLab** (PRs), and **Context7** (current docs). At the start of a task, confirm
> Linear is connected and pointed at the right project/team — if it isn't, **flag it and
> don't start working blind**. Setup for all three is in the README.

---

## 1. The board is the source of truth — keep Linear current

Linear holds the truth about every task: its status, the discussion, the decisions, the
blockers. Slack is for quick pings and scheduling only.

- Keep **all task discussion on the Linear issue** — questions, findings, decisions,
  blockers. ❌ Don't bury it in a Slack DM or thread; it gets lost and is painful to dig
  up later.
- Linear is what we optimize for. Keep the issue's **status and details constantly
  current**, so anyone can see where things stand **without having to ask you**.
- We do **not** post daily progress write-ups, and you don't owe an end-of-day note —
  **we infer status from the board.** That only works if the board actually reflects
  reality. So make sure Linear is updated at all time. We judge output, not hours online.

## 2. Never wait idle — pull the next task

The Todo list in Linear is prepped ahead of each week. Those tasks are yours to pull.

- The moment you finish or get blocked, **pick the next Todo item and keep moving.**
- You do not need to wait to be assigned work. If it's in Todo, it's fair game.
- ✅ Blocked on access or a decision? Drop the blocker on the issue, then grab the next
  Todo and stay productive. Also update the status of the task as Blocker, so it get's the attention it deserves.
- ❌ Sit and wait on a reply while a dozen ready tasks go untouched.

## 3. Surface blockers fast

- If something will cost more than ~30 minutes of waiting, raise it **now** — as a comment
  on the issue, tagging whoever can unblock it. Then switch tasks (see #2).
- ❌ Absorb a blocker silently for hours. ✅ Flag it in minutes and move on.

## 4. Don't stall on planning — build the cheap thing, ask only on the expensive calls

Code is cheap to write _and_ rewrite, especially with AI. A working thin slice usually
beats a planning round-trip: it's faster, and people give a sharper decision on something
concrete than on an abstract plan.

- For **reversible, low-stakes** work, just build a small version and show it. Don't wait
  for sign-off, and don't write a big plan first.
- **Plan up front only for big tasks** — large scope, many moving parts, or hard to undo.
  There, a written plan reviewed before you build is worth it. The smaller the task, the
  less planning it needs.
- Reserve a decision-ask for what stays expensive even when code is cheap: **product/scope
  direction, hard-to-reverse changes** (schema/data migrations, public APIs, client-facing
  commitments), or **anything that blocks teammates**.
- When you do need a call, make it **1–3 high-level bullets with your recommendation** —
  short enough to approve in seconds.
  ✅ "For v1 I'd go with simple tracking over full fulfillment automation because X — confirm?"
  ❌ a long plan that's slow to read and blocks everyone waiting on it.
- While you wait on any answer, **pull the next task** (see #2). Don't sit idle.

## 5. Branch & PR hygiene — open a PR early

- Branch off `dev` (or the repo default). **One branch per task — docs and code together.**
  Put the doc/plan link on the Linear issue so it all points to one place.
- **Open a draft PR as soon as the branch exists.** Work sitting in a local branch with no
  PR is invisible — the open PR is what shows the team, on GitHub, which tasks are in flight.
- Share the **PR link**, never a raw GitHub file or commit URL.
- Mark a PR **"Ready for review" only after you've tested it yourself.** If you deliberately
  left something out, say so explicitly and link a tracking issue — don't let review catch it.

## 6. Communicate concise and client-ready

- Anything that might reach a client: **1–3 bullets, plain language, with your recommendation.**
  No raw technical dumps.
- If you can't compress it, that's the signal you haven't yet decided what matters. Decide
  first, then send.

---

## The one-line version

> **Board is truth · Pull, don't wait · Flag blockers fast · Build cheap, ask only on the
> big calls · Open a PR early · Test before "ready" · Speak in bullets.**

## Why this exists

These are the same few things we kept repeating across projects. Putting them here means
they live in one place the agent surfaces automatically — so the working style is the same
for everyone, on every project and client, without anyone having to hold it in their head.
