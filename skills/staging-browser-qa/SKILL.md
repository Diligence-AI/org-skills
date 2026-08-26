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

## Staging account access

Reuse an authorized browser session or an operator-provided account when one is
available. If neither is available, create a temporary non-privileged account through
the staging application. Use a synthetic test identity and generate its password
without printing or committing it. Do not depend on a default seed account because a
repository might not provide one.

Stop and ask the operator when signup needs an inbox or verification step that the
agent cannot access, or when the feature needs privileges or existing test data that a
new account does not have. Never create a privileged account or read password hashes,
session tokens, or verification tokens from the database. Write directly to a database
only with explicit operator approval because that bypasses the application workflow.

## Workflow

1. Read the issue, accepted clarifications, acceptance criteria, and feature diff.
2. Confirm that the staging branch contains the feature and that the exact commit has
   a ready deployment at the configured staging URL.
3. Stop if the commit, domain, environment, or database may be wrong or production.
4. Make a focused checklist only from the issue, accepted clarifications, and feature
   diff. Test the changed user flows and required edge cases. Do not add a fixed
   project-wide smoke suite.
5. Use the configured staging account policy and the staging account access rules above.
6. Run the checklist with agent-browser. Take a new snapshot after navigation or a
   major page update because old element references can become invalid.
7. Capture useful screenshots. Record a WebM video when a multi-step flow is easier
   to review in sequence. Do not capture secrets or private user data.
8. Close the browser session. Report the tested commit, staging URL, scenarios,
   failures, artifact paths, and remaining risk on the Linear issue.
9. Tag the configured human QA owner only after the automated checks pass. Do not
   deploy production or mark human QA complete.

Stop and report a blocker when the feature is not deployed, the deployment is not
ready, the permitted account paths cannot provide access, the main flow fails, or
testing needs an unapproved external or database change.
