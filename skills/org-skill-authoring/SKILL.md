---
name: org-skill-authoring
description: >-
  Creates, edits, validates, reviews, and publishes skills in the Diligence AI
  org-skills repository. Use when asked to create or update an org skill, change
  how-we-work, or raise an org-skills PR. Keeps org-skill PRs ready for review and
  applies merged skills to the authoring environment or hands off that install.
---

# Org Skill Authoring

Use `/srv/workspaces/diligence-ai/org-skills` as the source repository. Edit source skills,
not an installed copy. Read the matching `skills/<name>/SKILL.md` before changing an existing
skill, then read [writing-skills](../writing-skills/SKILL.md) before authoring.

## Author and review

1. Keep one capability per skill. Use `how-we-work` only as the lightweight workflow index.
2. Add each new skill to the `## Skills` index in `README.md` so teammates can discover it.
3. Validate each changed skill with the available skill validator and inspect the complete
   diff for unrelated changes, private names, and proprietary examples.
4. Use authenticated `gh` directly to open or update the PR.
5. Do not leave an org-skills PR in draft. Complete the authoring checks, then open it as
   ready for review or mark the existing PR ready.

## Apply a merged skill

After the PR merges, use the current install command in `README.md` to install the merged org
skills in the environment that will use them, then verify the installed copy matches the
merged source. Skills do not hot-reload, so tell the operator to start a new chat or session
when discovery or behavior must use the new version.

If another chat or agent owns the authoring environment, send it the merged PR link and commit
with a direct request to install and verify the merged skills. Do not claim that the update is
active until that install or handoff is confirmed.
