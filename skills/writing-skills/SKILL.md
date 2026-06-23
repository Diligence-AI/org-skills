---
name: writing-skills
description: >-
  Best practices for authoring, editing, and reviewing Agent Skills (SKILL.md
  files). Consult whenever someone asks to "write a skill", "create a skill",
  "improve a skill's description", "review a SKILL.md", or audit why a skill
  isn't triggering. Covers frontmatter, the description-as-trigger spec,
  progressive disclosure, body voice, testing, and anti-patterns. Do NOT trigger
  for ordinary docs, READMEs, or non-skill markdown.
---

# Writing Agent Skills

A skill is a folder the agent loads on demand to gain a capability. Most skills fail in one
of two ways: the agent never finds them (bad description), or it finds them and gets bad
instructions (bloated, vague, or railroading body). This doc is for both. It practices what
it preaches — read it as a worked example.

> Golden rule: **the context window is a public good.** Every line you add is read on every
> trigger, so only add what the model doesn't already know. Restating defaults wastes the
> budget you need for the parts that matter.

---

## 1. Format & frontmatter

- One skill per directory: `skills/<name>/SKILL.md`. The `name` **must** equal the
  kebab-case directory name — discovery keys off the path, so a mismatch makes the skill
  unloadable.
- `name`: lowercase + hyphens, ≤64 chars, no `claude`/`anthropic` (reserved — rejected by
  the loader).
- `description`: required, ≤1024 chars. This is the highest-leverage field (see §2).
- `name` + `description` are the only required keys. Everything else is optional:

| Optional key | Use it for |
|---|---|
| `license`, `metadata.{author,version,tags}` | Provenance / versioning |
| `allowed-tools` | Scope tools, e.g. `Bash(npx shadcn@latest *)` — narrow so the skill can't run arbitrary commands |
| `user-invocable: false` | Internal skill, hidden from the slash menu |
| `disable-model-invocation: true` | Only fires when explicitly invoked, never auto |
| `argument-hint`, `model`, `effort` | Slash-command UX and runtime hints |

---

## 2. The description is a trigger spec (≈80% of the effort)

At startup only `name` + `description` load (~100 tokens/skill); the body is **not read
until the description matches.** So the description alone decides whether the skill ever
fires. Spend your effort here.

- **Third person, always.** "Processes Excel files…" — never "I can help…" or "You can
  use this…". Mixed point-of-view degrades matching.
- Pick one of two styles by whether the trigger has a checkable right answer:
  - **(A) Trigger-phrase stuffing** — for objective skills (file types, named APIs). Quote
    literal phrases users type, list file extensions, and add negative boundaries
    ("Do NOT trigger when…") to stop false fires.
  - **(B) Terse capability statement** — for subjective/judgment skills where any
    enumeration would be arbitrary.
- **Be slightly pushy.** Models tend to *under*-trigger, so err toward inclusion and pack
  in the keywords/extensions a user would actually type.

Good vs bad:

```
BAD:  description: Helps with documents.          # vague — the #1 anti-pattern, never fires
GOOD: description: >-
        Extracts tables and text from PDF, DOCX, and XLSX files. Triggers on
        "parse this PDF", "pull the table out of", file extensions .pdf/.docx/.xlsx.
        Do NOT trigger for plain .txt or markdown.
```

---

## 3. Progressive disclosure — three levels

The whole design is "load metadata always, load detail on demand." Respect the levels:

1. **L1 — metadata** (`name`+`description`): always in context, ~100 tokens. Keep it tight.
2. **L2 — SKILL.md body**: loaded on trigger. Keep **under ~500 lines / ~5k tokens** — past
   that the model skims and misses instructions.
3. **L3 — bundled files** (`references/`, `scripts/`, `assets/`): loaded only when the model
   reads them. Effectively unbounded, **zero cost until used** — push bulk here.

Rules that keep L3 working:

- Keep references **one level deep** from SKILL.md — models partial-read nested chains and
  silently lose the tail.
- For any reference file >100 lines, add a table of contents so partial reads still orient.
- When you point at a file, **name it, say WHEN to load it, and summarize what's inside** —
  otherwise the model won't know it's worth the read.
- Know the difference: **references get read; templates get copied.** Swapping them (a
  template the model reads, or a reference it copies verbatim) is a classic bug.

Architectures seen in production — pick by shape, don't cargo-cult:

- **Inline-everything** (Supabase): all in SKILL.md; fights agent laziness, good for small scope.
- **Thin router → ref files** (Stripe): SKILL.md dispatches to L3.
- **Index over rule-files** (Vercel, Cloudflare, shadcn): SKILL.md is a map to many small docs.
- **Remote/CLI-served stub**: SKILL.md just tells the agent to call a tool/CLI for the rest.

---

## 4. Writing the body

- Imperative voice. Numbered steps for workflows; copyable `- [ ]` checklists for multi-step
  operations so the agent can track them.
- **Pair every constraint with its consequence.** This is the single most consistent
  technique across good skills. A rule without a reason gets overridden the moment it's
  inconvenient; a rule with a reason holds.

  ```
  BAD:  Never use Unicode subscripts.
  GOOD: Never use Unicode subscripts — the built-in fonts lack these glyphs, so they
        render as solid black boxes.
  ```

- **Explain the why; don't railroad.** All-caps MUST/NEVER is a yellow flag. Spend it ONLY
  where a wrong answer is *silently corrupt* — migrations, financial models, fragile APIs.
  (Anthropic's frontend-design skill has zero MUSTs and is one of their most-used.)
- **Match degrees of freedom to fragility.** Open-ended task → plain prose, let the model
  reason. Fragile task → exact script with "do not modify this command." Over-constraining
  open work makes the model worse; under-constraining fragile work breaks it.
- **For API/library skills, distrust stale training data.** Tell the model its knowledge may
  be outdated and *how* to get current docs (Context7, append `.md` to a docs URL, read the
  changelog). Near-universal in company skills because APIs drift.
- Consistent terminology (one name per concept), forward-slash paths, and **no
  time-sensitive info** — "currently", version numbers, "new in vX" all rot. Park
  deprecated guidance in a collapsed "old patterns" section instead.

Distinctive techniques worth reaching for:

- **Taste-as-data**: concrete hex palettes / font pairs beat vague adjectives like "modern".
- **Negative anchoring**: name the cliché to avoid ("not another purple-gradient SaaS hero").
- **ASCII decision trees** keyed on user intent for branchy workflows.
- **Coined leading words** and role-play priming to set a consistent stance.
- A **"Gotchas" section** built from real observed failures, not imagined ones.

---

## 5. Testing & iteration

- **Eval-first.** Run the task *without* the skill, document exactly how it fails, write ≥3
  concrete scenarios, then add the *minimum* instructions that make them pass. Skip this and
  you'll write rules for problems that don't exist while missing the ones that do.
- **Two-Claude loop.** Claude A authors; a *fresh* Claude B tests. Watch navigation: if B
  re-reads a reference file, that content belongs in SKILL.md; if B never reads a file, cut
  it.
- **Skills don't hot-reload.** Edits are invisible mid-session and new skills are discovered
  only at session start — so restart between test runs, and **version-control the skills
  folder** or you'll lose the working version.

---

## Anti-patterns checklist

- [ ] Vague or first-person description (the top cause of a skill never firing)
- [ ] Under-triggering — too few keywords / no literal user phrases
- [ ] Mega-skill doing many jobs — split it; one skill, one job
- [ ] Railroading with rigid MUSTs where a wrong answer isn't actually corrupt
- [ ] References vs templates swapped (one read, the other copied)
- [ ] Too many options — give one default plus an escape hatch
- [ ] Time-sensitive info baked into the body
- [ ] Inconsistent terminology for the same concept
- [ ] Deeply nested references (>1 level deep)
- [ ] Windows backslash paths
- [ ] Scripts that swallow errors or hide magic constants
- [ ] Overfitting instructions to a handful of test cases

---

## TL;DR

> Nail the third-person description (that's the trigger) · push bulk into L3 references ·
> keep the body lean and imperative · pair every rule with its consequence · MUSTs only
> where a wrong answer corrupts · eval-first, test with a fresh agent.
