# Diligence AI — Org Skills

Shared, installable skills that encode **how our team works**. Install once and your
coding agent (Claude Code, Codex, Cursor, etc.) surfaces the rules automatically — so the
working style is the same on every project and client, and nobody has to keep it in their head.

## Skills

- **how-we-work** — our operating ethos: board-is-truth (Linear), pull-don't-wait,
  flag blockers fast, build cheap & ask only on the big calls, open a PR early,
  test before "ready", concise client-ready comms.
- **create-linear-task** — creates source-faithful Linear tasks, checks related work, and
  preserves supplied attachments without adding inferred scope.
- **external-code-review** — runs a fresh, read-only Claude review with the requested Opus
  or Fable model and waits for the paid review to finish.
- **staging-browser-qa** — verifies a completed feature on its deployed staging commit
  with agent-browser, captures review evidence, and prepares the human-QA handoff.

## Install (every team member, once per machine)

Install the Diligence org skills:

```bash
npx skills@latest add Diligence-AI/org-skills
```

Also install the recommended grill companion skills from
[Matt Pocock's skill library](https://github.com/mattpocock/skills):

```bash
npx skills@latest add mattpocock/skills --skill grilling grill-me grill-with-docs -y
```

These install into your agent's skills directory (e.g. `~/.claude/skills/` and
`~/.codex/skills/`) and work with any SKILL.md-compatible agent (Claude Code, Codex,
Cursor, …).

## Recommended companion skills

The org skills encode how Diligence works. Matt Pocock's skill library adds useful working
modes that help teammates pressure-test plans and explore design options.

Start with the grill skills:

- **[grilling](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md)**,
  with **[grill-me](https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md)**
  as its short pointer, plus
  **[grill-with-docs](https://github.com/mattpocock/skills/blob/main/skills/engineering/grill-with-docs/SKILL.md)**,
  to pressure-test a plan or design before building; use the docs variant when ADRs or
  glossary entries should be captured.

Test these separately before making them default workflow recommendations:

- **decision-mapping** — turn a vague request into sequenced investigation tickets.
- **design-an-interface** — compare multiple API/module shapes before committing.
- **handoff** — compact context so another teammate can continue cleanly.
- **improve-codebase-architecture** — scan a codebase for structural improvement options.
- **tdd** — drive implementation through tests when behavior needs to stay tight.
- **teach** — explain a concept or workflow inside the current workspace.

These do not replace **how-we-work**. Use the org skills for team operating rules, then
invoke companion skills for a specific work mode.

## Prerequisites — connect MCPs, authenticate GitHub, and install browser tooling

The **how-we-work** skill assumes your agent can reach the tools the workflow runs on. Connect
or install these tools in the agent environment (one-time setup per machine), before you start
work:

- **Linear MCP** — the live source of truth for all work. Authenticate it and point it at
  the **right project/team**. Use its tools directly for issue reads and writes, status
  changes, comments, and task operations. Do not route Linear work through a generic wrapper
  CLI or task proxy. Without it, status, tasks, and blockers can't flow through the board and
  the ethos doesn't work — so the skill will ask you to fix it before starting.
- **GitHub `gh` CLI** — install and authenticate `gh` in the environment where the agent runs.
  Confirm access with `gh auth status`, then use `gh` directly for GitHub operations such as
  draft PR creation and review. Do not use a generic wrapper CLI or task proxy. The
  authenticated account's existing repository permissions are the boundary; do not bypass
  access controls.
- **GitLab (only for GitLab repositories)** — if the repository uses GitLab, connect its
  configured authenticated GitLab tooling for PR operations. GitHub repositories do not
  require GitLab setup.
- **Context7 MCP** — pulls current library/framework docs while you build, so the agent
  works against up-to-date APIs instead of stale training data.
- **agent-browser CLI** — install it in the environment where the agent runs, such as
  the remote workspace or container. Installing it only on the operator's computer does
  not make it available to a remote agent.

For Claude Code, add the MCP servers to your MCP config and install/authenticate `gh`; other
agents have their own MCP and CLI setup.

## Updating

Edit a skill here, commit, and push. Teammates re-run the install command to pull the
latest. One edit propagates to everyone.

## Onboarding

Add both install commands above to the new-hire checklist. That's the whole setup.
