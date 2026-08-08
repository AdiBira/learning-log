# learning-log

A skill that quietly keeps a running log of the technical concepts you **genuinely learn** —
captured the moment they click, not when you remember to write them down.

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

**Manual:** copy `SKILL.md` into your skills directory, e.g.

    ~/.claude/skills/learning-log/SKILL.md

That's it. The skill self-triggers whenever you're learning; nothing else to configure.

## Log format

    - [x] **{concept}** | {project} | {date} | {one-line explanation}

The explanation is pitched at the depth you engaged at, so a companion review skill can
re-teach each concept at the same level later.

## Optional: always-on capture via a hook

The skill triggers from conversation context, which covers the vast majority of learning.
If you want *guaranteed* capture regardless of context — at the cost of a bit more overhead —
add a `Stop` hook in your harness that re-runs the sweep at the end of every session. This is
opt-in and not bundled, because an always-on hook is invasive for a shared skill; add it only
if you want zero-effort passive capture.

## Pairs with

A review skill (spaced repetition) can read recent entries and **re-teach** each concept at
its original depth, then optionally quiz you. Kept separate so capture stays lightweight.

## License

MIT
