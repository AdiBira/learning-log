---
name: learning-log
description: >
  Silently capture technical concepts the user genuinely learns into a running log, the
  moment they learn them. Use continuously — not on demand — during any conversation where
  the user is building understanding: asking "what is X / how does X work / why is X",
  or debugging, configuring, tuning, or reasoning through a mechanism until it clicks.
  Do NOT use for concepts merely mentioned, tools or code merely used, or generated output
  merely accepted. Triggers across any domain: tech, science, finance, hardware, anything.
---

# Learning Log

Maintain a running log of technical concepts the user has **genuinely learned** — one line
each — so their learning is captured as it happens, not lost to memory or context summaries.

Default log path: `~/learned-log.md` (or your harness's user-config dir, e.g.
`~/.claude/learned-log.md`). Create it with a header if missing.

> Model-agnostic: the instructions below are plain and work with any capable LLM. Where a
> harness auto-loads Agent Skills, this triggers itself; where it doesn't, paste this body
> into the system prompt.

## Log continuously, while learning — never wait for "the end"

Append the moment a concept lands. Do not batch to end-of-session: long sessions get
summarized and early learning is lost; writing to disk immediately preserves it at full
fidelity. This behavior stays active for the rest of the conversation once triggered.

## When to log

Append an entry when ANY of these hold:

1. **Explicit ask** — the user asked "what is X", "how does X work", "why is X".
2. **Learning-by-doing** — the user debugged, configured, tuned, or worked through a
   mechanism and visibly built understanding (follow-up questions, "oh, so it's...",
   correcting their own mental model). This kind of learning has no single question moment;
   it emerges across the exchange. Catch it.
3. **Engaged-with** — the user pushed back on, asked to go deeper on, or reasoned about
   something raised in the conversation.

## When NOT to log (noise guard)

- **Used, not learned.** Code or tools the user directed but did not open and understand.
  Iterating on generated *output* (tuning a design, accepting generated code) is using, not
  learning. Log only if the user engaged with HOW it works — the mechanism, not the result.
- Concepts mentioned in passing with no engagement.
- Project-specific decisions, file names, one-off commands, config values.

**Litmus test — could the user now explain this to someone else?**
Saw the output work → no, don't log. Reasoned about the mechanism → yes, log.

## Entry format

Append exactly one line per concept:

    - [x] **{concept}** | {project} | {date} | {one-line explanation}

- `{concept}` — the term/idea, specific (e.g. "NumPy broadcasting", not "arrays").
- `{project}` — the repo, workspace, or topic in focus (infer from context).
- `{date}` — today, `YYYY-MM-DD`.
- `{explanation}` — under 25 words, and pitched at **the depth the user actually engaged
  at**, so it can later be re-taught at the same level. Not a dictionary gloss; the working
  understanding they reached.

Example lines (illustrative):

    - [x] **NumPy broadcasting** | myapp | 2026-01-15 | A smaller array is auto-stretched to operate elementwise against a larger one, no explicit loop.
    - [x] **Idempotency keys** | webscraper | 2026-01-15 | A client-supplied token that makes a retried POST apply once, so network retries don't double-charge.

## Rules

- **No duplicates** — scan existing entries before appending; skip anything already logged.
- **Silent** — never announce a log write; keep the conversation flowing.
- **One canonical tag per project** — don't split the same project across spellings.

## Optional wrap-up glance

When a learning-heavy topic clearly wraps, take one look back for learning-by-doing that no
single question captured, and log those too. This is a supplement to continuous logging — a
safety net for diffuse learning — not the main mechanism.
