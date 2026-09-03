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

## Apply a pushed skill

After the push, use the current install command in `README.md` to install the org skills in
the environment that will use them, then verify the installed copy matches `main`. Skills do
not hot-reload, so tell the operator to start a new chat or session when discovery or
behavior must use the new version.

If another chat or agent owns the authoring environment, send it the pushed commit on `main`
with a direct request to install and verify the skills. Do not claim that the update is active
until that install or handoff is confirmed.
