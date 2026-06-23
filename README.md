# Diligence AI — Org Skill

Shared, installable skills that encode **how our team works**. Install once and your
coding agent (Claude Code, Codex, Cursor, etc.) surfaces the rules automatically — so the
working style is the same on every project and client, and nobody has to keep it in their head.

## Skills

- **team-ethos** — our operating ethos: board-is-truth (Linear), pull-don't-wait,
  flag blockers fast, plan → review → build, test before "ready", concise client-ready
  comms, own your judgment.

## Install (every team member, once per machine)

```bash
npx skills add Diligence-AI/diligence-ai-org-skill
```

This drops the skills into your agent's skills directory (e.g. `~/.claude/skills/` and
`~/.codex/skills/`). They work across SKILL.md-compatible agents.

## Updating

Edit a skill here, commit, and push. Teammates re-run the install command to pull the
latest. One edit propagates to everyone.

## Onboarding

Add the install command above to the new-hire checklist. That's the whole setup.
