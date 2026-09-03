---
name: org-skill-authoring
description: >-
  Creates, edits, validates, and publishes skills in the Diligence AI org-skills
  repository. Use when asked to create or update an org skill or change how-we-work.
  Commits and pushes org-skill changes straight to main, then applies them to the
  authoring environment or hands off that install.
---

# Org Skill Authoring

Use `/srv/workspaces/diligence-ai/org-skills` as the source repository. Edit source skills,
not an installed copy. Read the matching `skills/<name>/SKILL.md` before changing an existing
skill, then read [writing-skills](../writing-skills/SKILL.md) before authoring.

## Author and publish

1. Keep one capability per skill. Use `how-we-work` only as the lightweight workflow index.
2. Add each new skill to the `## Skills` index in `README.md` so teammates can discover it.
3. Validate each changed skill with the available skill validator and inspect the complete
   diff for unrelated changes, private names, and proprietary examples.
4. Commit and push to `main` directly. This repo uses no pull request and no reviewer.
   Keep each commit to one change, so a `git revert` is a clean undo.
5. `main` is not protected and there is no CI, so complete the checks in step 3 before you
   push. Nothing downstream will catch a broken skill.
6. Install immediately after the push, in the same turn. A pushed skill that is not
   installed changes nothing; the agent keeps following the old copy. See
   [Install after every push](#install-after-every-push).

## Install after every push

Never stop at the push. Run the install in the same turn:

```bash
export PATH="$HOME/.nvm/versions/node/$(ls "$HOME/.nvm/versions/node" | tail -1)/bin:$PATH"
npx --yes skills@latest add Diligence-AI/org-skills
```

`npx` is not on the default `PATH` on this host, so set it as shown or the command fails with
`command not found`.

Then verify, and do not claim the update is live until this passes:

```bash
git show origin/main:skills/<name>/SKILL.md | diff - ~/.claude/skills/<name>/SKILL.md
```

Check any new `references/` file the same way. The installer overwrites each skill folder it
owns and leaves unrelated local skills alone, but back up `~/.claude/skills` first when the
install has not been run on a machine before.

The agent's loaded skill list refreshes after the install, so the new version takes effect in
the running session. If a change to a `description` does not show up, start a new session,
because discovery reads descriptions at session start.

If another chat or agent owns the authoring environment, send it the pushed commit on `main`
with a direct request to install and verify the skills. Do not claim that the update is active
until that install or handoff is confirmed.
