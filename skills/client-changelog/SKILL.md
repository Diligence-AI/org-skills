---
name: client-changelog
description: >-
  Writes short, client-safe changelog entries for product fixes and updates.
  Use when asked for client update language, a client-facing fix summary,
  release notes, or changelog text. Do not use for internal engineering logs
  or technical postmortems. For general client messages, use client-communication.
---

# Client Changelog

Write one short sentence unless the user asks for more detail.

- State the result that the client will notice. Add the condition that caused the problem
  only when it makes the update clearer.
- Use plain words and past tense. A useful pattern is:
  `Fixed [feature] errors when [condition].`
- Keep private details private. Omit client and account names, issue IDs, code, SQL, stack
  traces, root-cause analysis, and internal project names. Use a product or feature name
  only when it is already client-facing and needed for clarity.
- Do not claim that a fix is deployed or complete unless the supplied evidence confirms it.

Example: `Fixed sync errors when no records were found.`
