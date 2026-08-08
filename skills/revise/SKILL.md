---
name: revise
description: Re-teach concepts from a learning log at the depth originally captured, then optionally test recall and revisit gaps. Use when the user asks to revise, review, relearn, practice, practise, or be quizzed on concepts they learned recently; requests spaced repetition from their learning log; or names a project, topic, or date range to review. Keep quizzes about learned concepts inside this skill. Do not use for quizzes about understanding a code change before merging or shipping.
---

# Revise

Turn captured learning into durable understanding. Re-teach by default; test only when the
user asks for a quiz, active recall, or a combined session.

## Find the learning log

Use the path the user gives. Otherwise, inspect an installed `learning-log` skill for its
configured path, then try `~/learned-log.md` and the harness's user-config directory (for
example, `~/.claude/learned-log.md`). If no log exists, say so and ask for its location.
Never invent entries or silently create an empty log.

Parse entries shaped like:

    - [x] **{concept}** | {project} | {date} | {one-line explanation}

## Select concepts

Honor any topic, project, date range, or count the user specifies. Otherwise:

1. Select up to five concepts learned in the last seven days.
2. Prefer concepts that have not been reviewed, then concepts previously marked `partial`
   or `missed` in the sibling review-history file.
3. If the last seven days contain nothing, use the five most recent entries and tell the
   user that the range was widened.
4. Keep distinct concepts separate and collapse exact duplicates.

## Match the original depth honestly

Treat each entry's explanation as the evidence of the depth reached. Match its conceptual
granularity and vocabulary; do not inflate a short working insight into an expert lecture.
Use the original conversation or linked notes when available to recover more detail.

A one-line entry cannot preserve an exact earlier explanation. Never claim verbatim or exact
fidelity when the source context is unavailable. Reconstruct the smallest useful explanation
that restores the logged mental model, and offer to go deeper.

## Choose the session mode

### Re-teach (default)

For each concept, give:

1. The core idea in plain language.
2. The mechanism or causal intuition at the logged depth.
3. One compact example or contrast only when it helps restore the mental model.

Teach related concepts together, but keep the session easy to scan. Do not turn the session
into a quiz unless the user asks.

### Active recall

Ask one question at a time before showing the answer. Make every question answerable from the
understanding represented in the log; test mechanisms and application, not trivia or wording.

After each answer:

- Mark it `correct`, `partial`, or `missed`, with one sentence of concrete feedback.
- Re-teach only the missing or mistaken part at the logged depth.
- Let the user retry once after a `partial` or `missed` answer.
- Continue only after the user answers; never simulate their response.

### Re-teach + recall

Re-teach the selected concepts first, then ask a short application question for each. Warn
that this checks immediate comprehension; question-first active recall is a better measure of
retention.

## Track reviews

After a recall session, append one line per tested concept to a sibling review-history file:
add `-reviews` before the learning log's extension (for example, `learned-log.md` becomes
`learned-log-reviews.md`).

    - **{concept}** | {project} | learned {date} | reviewed {date} | {correct|partial|missed}

Use the most recent result when prioritizing later sessions. Do not alter the source learning
log. Do not record a result for re-teaching alone or for an unanswered question.

## Boundaries

- Do not add facts unrelated to restoring the logged understanding.
- Do not confuse familiarity after re-reading with successful recall.
- Do not shame weak answers or soften incorrect ones.
- Do not use this workflow to gate a code merge; a code-comprehension or pre-ship quiz is a
  separate purpose.
