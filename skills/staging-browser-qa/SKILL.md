---
name: staging-browser-qa
description: >-
  Tests a completed feature in staging with agent-browser. Use when asked to
  "test this on staging", "QA this feature", "verify staging", "run browser
  QA", or "record a staging demo" after the feature reaches the staging branch.
  Confirms the deployed commit, runs focused browser checks, captures evidence,
  and prepares the human-QA handoff. Do not use for production deployment, load
  testing, or general release management.
---

# Staging Browser QA

Test the changed feature as a user. Treat deployment as a short entry check.

## Runtime requirement

Confirm that the `agent-browser` CLI is installed in the environment where the agent
runs. If it is unavailable, stop and report the setup blocker. Do not replace browser
QA with source-code inspection.

## Repository settings

Read `docs/staging-browser-qa.md` in the active repository. If the file or a required
value is missing, ask the operator. Do not guess. Keep client names, domains, account
details, and other repository-specific information out of this shared skill.

## Workflow

1. Read the issue, accepted clarifications, acceptance criteria, and feature diff.
   Decide whether the work is a **new feature** or a **bug fix**. The evidence and the
   report tell a different story for each: a feature shows what is new, step by step;
   a fix shows the problem, the fix, and how it was checked.
2. Confirm that the staging branch contains the feature and that the exact commit has
   a ready deployment at the configured staging URL.
3. Stop if the commit, domain, environment, or database may be wrong or production.
4. Make a focused checklist only from the issue, accepted clarifications, and feature
   diff. Test the changed user flows and required edge cases. Do not add a fixed
   project-wide smoke suite.
5. Use the configured staging account policy. Never expose credentials, create a
   privileged account, or write directly to a database without explicit approval.
6. Run the checklist with agent-browser. Take a new snapshot after navigation or a
   major page update because old element references can become invalid.
7. Capture evidence as described in [Evidence](#evidence). Do not capture secrets or
   private user data.
8. Close the browser session. If the `qa-report` skill is available, use it to publish
   the evidence and post its one report link. Otherwise report the local artifact paths.
   In both cases, report the tested commit, staging URL, scenarios, failures, and
   remaining risk on the Linear issue.
9. Tag the configured human QA owner only after the automated checks pass. Do not
   deploy production or mark human QA complete.

Stop and report a blocker when the feature is not deployed, the deployment is not
ready, access is missing, the main flow fails, or testing needs an unapproved external
or database change.

## Evidence

Clients and QA reviewers judge the work from this evidence, so make it easy to read.

- Set the viewport before the first capture: `agent-browser set viewport 1920 1080`.
  Use `390 844` only when the feature is mobile-specific. The default viewport is
  1280x577, which gives small, unclear videos.
- Record one short video for each flow. Start it just before the first step of that
  flow. After `record start`, confirm that the session is still signed in, because
  recording opens a fresh browser context.
- Wait about one second after each click, fill, and page load (`agent-browser wait
  1000`). Video records at about 10 frames per second, so fast steps are unreadable.
- Take a full-page screenshot (`screenshot --full`) at each key state, and always at
  the point of a failure. Screenshots are what a reviewer looks at first.
- For a bug fix, capture the corrected behavior at the place where the bug appeared.
  Add a "before" capture only when the old behavior can still be shown safely.
- Save files in `qa/<ISSUE-ID>/` and name them `<NN>-<flow>-<pass|fail>.<ext>`, such
  as `01-sign-in-pass.png` or `03-create-event-fail.webm`. The number keeps flow order
  and the status shows the result without opening the file.
