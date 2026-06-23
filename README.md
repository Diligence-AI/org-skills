# Diligence AI — Org Skills

Shared, installable skills that encode **how our team works**. Install once and your
coding agent (Claude Code, Codex, Cursor, etc.) surfaces the rules automatically — so the
working style is the same on every project and client, and nobody has to keep it in their head.

## Skills

- **how-we-work** — our operating ethos: board-is-truth (Linear), pull-don't-wait,
  flag blockers fast, build cheap & ask only on the big calls, open a PR early,
  test before "ready", concise client-ready comms.

## Install (every team member, once per machine)

```bash
npx skills add Diligence-AI/org-skills
```

This drops the skills into your agent's skills directory (e.g. `~/.claude/skills/` and
`~/.codex/skills/`). They work across SKILL.md-compatible agents.

## Prerequisites — connect your MCPs

The **how-we-work** skill assumes your agent can reach the tools the workflow runs on. Connect
these MCP servers in your agent (one-time setup per machine), before you start work:

- **Linear MCP** — the live source of truth for all work. Authenticate it and point it at
  the **right project/team**. Without it, status, tasks, and blockers can't flow through the
  board and the ethos doesn't work — so the skill will ask you to fix it before starting.
- **GitHub / GitLab MCP** — for branch and PR work (principle #5: open a PR early, share the
  PR link). Connect it to the repo host your team uses.
- **Context7 MCP** — pulls current library/framework docs while you build, so the agent
  works against up-to-date APIs instead of stale training data.

For Claude Code, add each server to your MCP config; other agents have their own MCP setup.

## Updating

Edit a skill here, commit, and push. Teammates re-run the install command to pull the
latest. One edit propagates to everyone.

## Onboarding

Add the install command above to the new-hire checklist. That's the whole setup.
