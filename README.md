# learning-log + revise

Two model-agnostic skills that form a lightweight learning loop:

- **`learning-log`** quietly captures concepts you genuinely learn as they click.
- **`revise`** re-teaches those concepts at the captured depth and optionally tests recall.

Most learning trackers only catch what you explicitly ask ("what is X?"). This one also
catches **learning-by-doing** — the concept you finally understood by debugging it, tuning
it, or arguing with it — while filtering out things you merely *used*. Directing a code
generator and tweaking its output is using, not learning; the skill knows the difference.

## What it does

- Watches for genuine learning in conversation (asked, worked-through, or engaged-with).
- Appends one clean line per concept to your learning log.
- Applies a "used vs learned" noise guard and a litmus test: *could you now explain this to
  someone else?*
- Logs continuously and silently — no command to run, no interruption.

## Works with any LLM and harness

The skill body is plain natural-language instruction — nothing model-specific — so it runs
on any capable model (Claude, GPT, Gemini, Grok, Kimi, …).

- **Harnesses that auto-load Agent Skills** (Claude Code, Claude.ai, Codex, and skill-runner
  marketplaces): drop the folder in and it self-triggers from the `description`.
- **Any other harness / raw API:** paste the body of `SKILL.md` into your system prompt. The
  behavior is identical; only the auto-trigger differs.

The only harness-specific detail is the log path — set it to wherever your setup keeps
user files (default `~/learned-log.md`; Claude users may prefer `~/.claude/learned-log.md`).

## Install

**skills.sh:**

    npx skills add AdiBira/learning-log

The installer discovers both skills and lets you choose either or both. To request both
explicitly:

    npx skills add AdiBira/learning-log --skill learning-log --skill revise

**Manual:** copy both directories from `skills/` into your skills directory, e.g.

    ~/.claude/skills/learning-log/SKILL.md
    ~/.claude/skills/revise/SKILL.md

`learning-log` self-triggers while you build understanding. Invoke `revise` whenever you want
to review; neither skill needs a hook.

## Log format

    - [x] **{concept}** | {project} | {date} | {one-line explanation}

The explanation is pitched at the depth you engaged at, so `revise` can restore that level
later.

## Optional: always-on capture via a hook

The skill triggers from conversation context, which covers the vast majority of learning.
If you want *guaranteed* capture regardless of context — at the cost of a bit more overhead —
add a `Stop` hook in your harness that re-runs the sweep at the end of every session. This is
opt-in and not bundled, because an always-on hook is invasive for a shared skill; add it only
if you want zero-effort passive capture.

## Revise modes

- **Re-teach (default):** restore the mental model at the granularity saved in the log.
- **Active recall:** ask first, grade honestly, re-teach gaps, and retry.
- **Re-teach + recall:** explain first, then check immediate comprehension.

Quiz is a mode inside `revise`, not a third skill, because both actions select the same log
entries and share the same teaching depth and review history. A pre-merge quiz about a code
change is a separate use case and is intentionally out of scope.

The log's one-line explanation preserves conceptual depth, not a verbatim lesson. When the
original conversation is unavailable, `revise` reconstructs the smallest useful explanation
at that granularity instead of pretending it can reproduce the exact earlier wording.

## License

MIT
