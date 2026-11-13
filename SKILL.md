---
name: learning-log
description: >
  Quietly record substantial learning episodes as connected topics worth revisiting.
  Use when the user works through a topic in depth and demonstrates understanding.
  Brief questions, syntax clarifications, isolated insights, and completed tasks alone
  do not qualify, even when a small detail was correctly understood.
---

# Learning Log

Keep a short index of topics the user spent meaningful effort understanding and could
return to for a proper revision session. Applies across technical and non-technical subjects.

## Decide what deserves an entry

Log only when all three conditions hold:

1. **The episode has substance.** Assess the whole exchange, not each message. The user
   works through a connected topic: its mechanism, a worked problem or implementation,
   misunderstandings, consequences, or limitations. There must be meaningful development
   beyond a local answer. A definition, syntax fix, isolated prediction, or one or two quick
   clarifications normally falls short, even when understood correctly.
2. **Understanding is visible in the user's work.** Look for their own causal reasoning,
   worked steps, corrections, or justified application. Assistant explanations, elapsed time,
   repeated questions, agreement, and successful generated code do not establish learning.
   A concise but substantial worked account can qualify; message count is not a gate.
3. **The topic merits a return visit.** It supports a useful revision session about how
   connected ideas work together. Fold supporting definitions, syntax, examples, and caveats
   into that topic. Skip task status, vendor facts, configuration choices, and familiar
   knowledge used again.

When uncertain, skip. Do not interrupt the user's task with a quiz to manufacture evidence.
Do not infer understanding from an assistant explanation, a successful tool call, or a
retrospective log entry. Backfilling requires the original conversation or the user's own
account of what they understood.

## Consolidate before writing

Wait until the local explanation or worked example resolves, then write promptly. Do not
wait for the whole session to end, and do not append after each follow-up question.

Choose a coherent topic at the scope actually understood. Working through tensor shapes,
filters, weight sharing, and pooling in a forward pass can produce one entry about CNN
forward-pass reasoning. It does not establish understanding of all neural networks.
Two quick questions about padding produce no entry. A brief dataclass clarification also
stays out; simply combining its details into one line does not make it substantial.

Keep genuinely separate substantial topics distinct. Do not combine unrelated learning
under a broad subject label. Within a topic, preserve the connections rather than listing
each component as another achievement. Unfinished work can qualify for the portion actually
understood; a blocker or claimed goal does not establish the missing understanding.

Read the existing log before writing. Match meaning, not just titles or project tags:

- If the topic and depth are already recorded, skip repetition and incidental elaboration.
- If the current exchange adds essential understanding to a directly related entry from
  this session, refine that entry rather than adding another. Retain its date and meaning.
- A substantial new layer can get a specifically scoped entry only when the whole episode
  passes the inclusion criteria. Reusing an idea in another project does not make it new.

Time and repeated engagement can support the depth judgment but never replace it. Zero
entries is normal. Do not use timers, message-count thresholds, quotas, target reduction
percentages, or a separate pending-entry database. Use the available conversation; do not
pretend to remember unseen earlier exchanges. Historical
bulk consolidation is a separate task requiring the user's request; preserve a backup and
do not invent evidence or dates.

## Store one line per substantial topic

Use the log path specified by the user or their instructions. Otherwise reuse an existing
`~/learned-log.md`, `~/.codex/learned-log.md`, or `~/.claude/learned-log.md`. If several exist
and none is designated, ask which is canonical rather than creating or merging copies.
If none exists, create `~/learned-log.md` with a `# Learned Concepts` header.

    - [x] **{concept}** | {project} | {date} | {explanation}

Use a stable project tag, the learning date in `YYYY-MM-DD`, and an explanation under
25 words. Name the topic specifically and summarize the connections actually understood,
not a list of keywords or a claim of mastery. The checkbox records a captured learning event,
not tested mastery. For historical learning with an unknown date, ask rather than guessing.

Example after a substantial worked CNN forward-pass episode:

    - [x] **CNN forward-pass reasoning** | ml-study | 2026-01-15 | Traced how kernel size, padding, stride, and pooling change feature-map dimensions while shared filters reuse learned patterns across positions.

Examples of capture decisions:

| Conversation | Action |
| --- | --- |
| User asks what backpropagation is; assistant explains; user changes topic | Skip: no demonstrated understanding |
| User correctly paraphrases frozen fields after a brief clarification | Skip: too shallow for a revision topic |
| User traces CNN shapes, corrects a pooling error, and reasons through a changed input | One scoped CNN forward-pass entry |
| User makes one correct prediction about clock drift | Skip: an isolated insight is insufficient |
| User diagnoses clock alignment through examples, distinguishing offset, drift, and jitter | One synchronization topic if substantive and new |
| An hour of generated work ends with user approval | Skip: duration and acceptance are insufficient |
| User says a delivered feature looks good | Skip: task acceptance |
| User applies an already logged idea in another repository | Skip: same mental model |

## Keep capture quiet and honest

Use normal file tools and verify that the intended line was saved. Do not announce successful
routine writes. If persistence is unavailable or fails, briefly say so; do not claim it was
saved. Do not silently substitute a different log path.

Keep personal entries separate from the skill package. Do not commit, upload, or publish
the log as part of installing, testing, or distributing the skill.

Automatic capture depends on the host loading this skill and providing writable storage.
This skill is not a background service and cannot guarantee capture in every chat. When
reviewing trends, report entries and coverage gaps, not learning speed or mastery.
