---
name: plan-before-code
description: >-
  Sets how to start an issue: find the real problem, check whether neighbouring
  issues share one root cause, name the problem type, and agree the approach
  before writing code. Use when picking up or being assigned an issue, before
  implementing a fix or a feature, when an estimate or a plan is requested, or
  when tempted to start coding straight from a ticket. Do not use as the Linear
  status procedure or the pull-request procedure.
---

# Plan Before Code

Writing code is the cheap part now. Understanding the problem is the work. Most of the effort
on an issue goes to understanding and agreement, and the remainder to implementation. A day
spent on the right approach costs less than a merged wrong fix, and far less than ten issues
that each solve the same thing a different way.

## Zoom out before you start

Read the landscape before the ticket. Look at the neighbouring issues, and at what already
runs on the default branch.

- When several issues share one foundational problem, say so. Propose fixing the root, and
  name the issues that then close, shrink, or wait.
- Never build a foundation that exists. Check the default branch first; extend what merged.
- An unmerged branch is evidence of what was tried, not a starting point. Read it for what to
  avoid, then start from what merged.

## Name the problem type

Classify the problem in computer-science terms — eventual consistency, duplication, ordering,
contention, a missing index — then choose the tool or framework that fits this codebase, and
cite the documentation behind the choice.

A named problem has known solutions. An unnamed problem gets a bespoke one.

## Agree before you build

Ask the questions that change the design before spending tokens on code, and ask the operator,
not yourself. Then state the problem as you understand it, propose the approach, and defend
it. Build after the approach is agreed.

Keep the hypotheses and the working notes on the branch, in a document. The issue gets one
pointer to that branch, and, after the decision, a short high-signal summary. See
[linear-workflow](../linear-workflow/SKILL.md).
