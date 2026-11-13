# learning-log

Keep a short record of the topics you worked through with an AI agent.

A useful learning session can span debugging, questions, wrong turns and worked examples.
Learning Log waits for that work to develop into something worth revisiting, then saves one
entry at the scope you actually understood.

Two questions about padding won't qualify. Tracing a CNN forward pass, correcting a shape
mistake and reasoning through a changed input can. Filters, padding and pooling belong in
that connected topic rather than becoming separate achievements.

## Install

```bash
npx skills add AdiBira/learning-log
```

Or copy this package into a `learning-log/` folder in your agent's skills directory. Start a
new session so the host can discover the updated instructions. Follow your host's skill
loading behavior; automatic invocation is host-dependent.

To make capture explicit in a session:

> Use learning-log as we work. Record substantial topics in my existing log; skip quick clarifications.

## What gets recorded

- A substantial learning episode with visible reasoning from you.
- One entry for a connected topic, with supporting details kept together.
- A short explanation of the connections and scope you understood.

Brief definitions, syntax questions, isolated insights and routine task facts are skipped,
even when a small detail was understood correctly. Time spent and message count don't earn
an entry by themselves. There is no daily quota or target reduction percentage.

```text
- [x] **CNN forward-pass reasoning** | ml-study | 2026-01-15 | Traced how kernel size, padding, stride, and pooling change feature-map dimensions while shared filters reuse learned patterns across positions.
```

Use your configured log path. If none is configured, the skill reuses an existing conventional
log or creates `~/learned-log.md`; it asks if multiple candidates make the choice ambiguous.
Your personal log stays separate from this distributable skill.

## Requirements and limitations

The host needs access to the current conversation and permission to read and write the chosen
Markdown log. No bundled scripts, dependencies, API keys, network access, or telemetry are
required. The instructions can also be used in a plain chat, but persistent saving requires
file tools.

Capture and judgment depend on the model and host. This is not a background service, a
complete conversation archive, or proof of retention. Missing dates mean missing records.
Existing history is not automatically rewritten. To audit or backfill learning, supply the
original conversations; old log lines alone cannot prove that understanding occurred.

## Review later

Ask your agent to show the recent entries or explain one again. The companion
[revise](https://github.com/AdiBira/revise) skill supports interactive review. It is installed
separately; this package only captures learning.

## License

MIT
