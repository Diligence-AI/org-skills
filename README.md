# Diligence AI — Org Skills

Shared, installable skills that encode **how our team works**. Install once and your
coding agent (Claude Code, Codex, Cursor, etc.) surfaces the rules automatically — so the
working style is the same on every project and client, and nobody has to keep it in their head.

## Skills

### Index

- **how-we-work** — the lightweight index for the focused Diligence workflow skills.

### Work tracking

- **linear-workflow** — keeps existing Linear work, blockers, review state, and next-task
  selection accurate.
- **create-linear-task** — creates source-faithful Linear tasks, checks related work, and
  preserves supplied attachments without adding inferred scope.

### Delivery

- **task-execution** — guides when to build, plan, request a decision, or switch tasks.
- **pull-request-workflow** — covers branches, PRs, self-review, QA, human review, and
  merge readiness.
- **external-code-review** — runs a fresh, read-only Claude review with the requested Opus
  or Fable model and waits for the paid review to finish.
- **staging-browser-qa** — verifies a completed feature on its deployed staging commit
  with agent-browser, captures review evidence, and prepares the human-QA handoff.

### Client communication

- **client-communication** — drafts concise client status, blocker, handoff, and decision
  messages.
- **client-changelog** — writes short, plain-language client changelog entries while
  keeping technical and proprietary details private.

### Skill maintenance

- **org-skill-authoring** — creates org skills, pushes them to `main`, and applies them to
  the authoring environment.
- **writing-skills** — guides skill descriptions, progressive disclosure, structure,
  testing, and review.

## Promotion bar

Skills in this repo are the team SOP. Answer three questions before a change lands:

1. **Useful beyond one project?** A lesson true only for one client repo stays in that repo.
2. **Safe to share?** No credentials, no client names or private details, no raw chat.
3. **Do we want everyone working this way?** The SOP changes slowly and deliberately.

All three yes → it lands. Anything else → it stays local (repo skill or personal layer).

Commit and push changes to `main` directly. There is no pull request step and no reviewer.
The author applies the bar above.

This repo has no CI, and `main` is not protected, so nothing else will catch a mistake.
Two habits carry the whole weight:

- **Keep each commit to one change**, so `git revert` is a clean undo.
- **Check a changed skill before you push it.** Valid frontmatter with `name` and
  `description`; every reference link points at a file that exists; any script in a
  reference file runs as written.

Teammates install with `npx skills add`, so a change on `main` reaches their machines on
their next install. Treat a push as a release.

## Install (every team member, once per machine)

Install the Diligence org skills:

```bash
npx skills@latest add Diligence-AI/org-skills
```

Also install the companion skills from
[Matt Pocock's skill library](https://github.com/mattpocock/skills). Pick **one** channel;
installing both leaves you with every companion skill twice.

On Claude Code, install the managed plugin. It carries all of the promoted skills and updates
when upstream ships:

```bash
claude plugins install mattpocock-skills
```

On Codex or any other SKILL.md agent, copy the skills we use into the repo:

```bash
npx skills@latest add mattpocock/skills --skill grilling grill-me grill-with-docs domain-modeling wayfinder -y
```

`grill-with-docs` calls `grilling` and `domain-modeling` through the Skill tool, so leaving
`domain-modeling` out gives you the interview with no glossary or ADRs.

These install into your agent's skills directory (e.g. `~/.claude/skills/` and
`~/.codex/skills/`) and work with any SKILL.md-compatible agent (Claude Code, Codex,
Cursor, …).

## Recommended companion skills

The org skills encode how Diligence works. Matt Pocock's skill library adds useful working
modes that help teammates pressure-test plans and explore design options.

Start with the grill skills:

- **[grilling](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md)**
  is the interview itself: it works a design tree in rounds, asks every question it can answer
  now, and attaches a recommended answer to each. Facts are the agent's job; decisions are
  yours.
- **[grill-me](https://github.com/mattpocock/skills/blob/main/skills/productivity/grill-me/SKILL.md)**
  is the short pointer to it. Use it when there is no working directory.
- **[grill-with-docs](https://github.com/mattpocock/skills/blob/main/skills/engineering/grill-with-docs/SKILL.md)**
  runs the same interview and adds
  **[domain-modeling](https://github.com/mattpocock/skills/blob/main/skills/engineering/domain-modeling/SKILL.md)**,
  which writes each agreed term to `CONTEXT.md` and each hard-to-reverse decision to an ADR as
  they land. Prefer it inside a repository: it leaves the paper trail the next session reads.

Then, for an effort too large to plan in one session:

- **[wayfinder](https://github.com/mattpocock/skills/blob/main/skills/engineering/wayfinder/SKILL.md)**
  charts a map of decision tickets on the issue tracker and resolves one per session, until the
  route to the goal is clear. It plans; it does not build, so hand its result to `to-spec` or
  straight to our delivery skills. It reads `docs/agents/issue-tracker.md`, so run
  `/setup-matt-pocock-skills` once per repository first and point it at Linear. Reach for it
  only when the route is genuinely not visible yet; a well-scoped feature wants
  `grill-with-docs` in one session instead.

Test these separately before making them default workflow recommendations:

- **codebase-design** — shared vocabulary for deep modules, and a design-it-twice pass that
  compares several interface shapes before committing.
- **handoff** — compact context so another teammate can continue cleanly.
- **improve-codebase-architecture** — scan a codebase for structural improvement options.
- **tdd** — drive implementation through tests when behavior needs to stay tight.
- **teach** — explain a concept or workflow inside the current workspace.

These do not replace the focused org workflow skills. Use **how-we-work** to select the
right org skill, then invoke companion skills for a specific work mode.

## Prerequisites — connect MCPs, authenticate GitHub, and install browser tooling

The org workflow skills assume your agent can reach the tools they use. Connect or install
these tools in the agent environment (one-time setup per machine) before you start work:

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

Add the org-skills install plus one companion channel to the new-hire checklist. That's the
whole setup.
