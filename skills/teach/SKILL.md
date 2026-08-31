---
name: teach
version: 1.3
description: Turns a moment of real work into one retained lesson, without breaking the session. Fires automatically the moment a session produces something teachable: an architectural decision, a technical pattern applied, a product judgment call, a book or case study cited, a metric or business model analysed. Emits one LEARN block, records the concept in a curriculum file, and seeds it into a spaced-repetition queue. Also runs on "/learn srs", "run my SRS review", "quiz me on what I learned", "teach me X". Do not use for mechanical edits, for a concept already logged this session, or as a substitute for the full explanation, which "teach me X" hands to the decoder skill.
---

# Teach

One session, one lesson, six lines. Small on purpose: a lesson that costs the session
its flow is not read twice.

## Plan first

Silently, before writing. Skipping it is a defect.

1. Done condition: one actionable block, plus the writes it implies.
2. Artifacts: the moment, the concept name, the block, the state changes.
3. Riskiest step: naming the concept. A wrong name links the lesson to nothing and it
   decays. Checked by finding the curriculum row first.
4. Execute. Print none of this.

## Read first

`references/local-context.md` if present. It names the learner, the curriculum file, the
review queue, the session log, the corpora, the observation log, and the skill that owns
full explanations. Absent, this skill still runs: emit the block, use `General` as the
cluster, and skip every write rather than inventing a path. Never guess a path, never
claim a write you did not make.

## Modes

| Mode | Trigger | Required input | Output | Done when |
|---|---|---|---|---|
| INJECT | a teachable moment fires in any session, no phrase needed | what just happened and why | one LEARN block, plus curriculum, queue and log writes | the block is placed and each write is made or explicitly skipped |
| REVIEW | "/learn srs", "run my SRS review", "quiz me" | the review queue | one question per due concept, then new intervals | every due row is passed, failed, skipped, or pruned |

One mode per invocation. INJECT never quizzes; REVIEW never emits a block.

## INJECT mode

**Is a moment.** An architectural decision with its reason on the record. A named
technical pattern applied. A product judgment call: a metric choice, an interface
trade-off, build against buy. A book, case study, or business model cited or analysed. A
tool or error pattern repeated three or more times. A concept that maps to a curriculum
row.

**Is not a moment.** A mechanical edit: rename, move, reformat, copy change. A concept
already logged this session. A concept too basic to add value. A clarifying question.


Contract:

1. **Scan the observation log** if local context names one and it exists. Repeated tool
   patterns and repeated errors are candidate moments. No log: read the session itself.
2. **Name the concept.** Find the curriculum row whose skill name best matches, and take
   its cluster number and exact skill name. No close match: cluster `General`, name
   `[concept], unlisted`. That is not a reason to skip steps 4 through 6.
3. **Write the block.** Shape below, exactly.
4. **Mark the curriculum row.** Unstarted becomes in-progress. Already in-progress or
   done: leave it. `General`: skip. One edit, nothing else.
5. **Seed the queue.** If the concept is not already in the review queue, append one row
   in the local-context format, due tomorrow, interval 1. Already present: skip.
6. **Log it.** One line in the session log: the concept name, then one sentence on what
   triggered it, including the session type.
7. **Promote a pattern, if one earned it.** Compare a repeated observation against the
   shared-pattern and past-mistake corpora. Confirms an entry: do nothing. Extends one,
   or is new and seen across two or more sessions: append a candidate in the local-context
   format. Contradicts a known pattern: say so in the session output, naming it.

### The block

```
💡 LEARN: [Cluster N: exact skill name | General: concept name]
[One sentence: the problem this exists to solve, stated before any definition]
[One sentence, two at most: the underlying principle or trade-off]
[One sentence: where this shows up for the audience named in local-context.md]
Connects to: [1 or 2 concepts already in the curriculum file, or "new branch"]
Say "teach me [skill name]" for the full breakdown
```

Hard stops, each of which blocks the block from shipping:

- **Exactly five lines after the header, six including it.** The header is not one of
  them.
- **Placement: after the session output, before the sign-off gate block.** The gate block
  is always the literal last block of a deliverable. This block never follows it.
- **The shape is fixed.** It is not the explanation ladder and is never restructured into
  it. When a session produces both, the ladder shapes the prose, this shapes the block.
- **Line 2 opens with the problem, never the definition.** "We used a webhook because
  polling wasted requests on a quiet stream" beats "a webhook is an event-driven
  callback".
- **`Connects to:` names concepts that exist.** Pull them from the curriculum file. An
  invented link is worse than "new branch": it makes the graph unfalsifiable.
- No em dashes and no arrow characters anywhere in the block.
- One block per session. Never the same concept twice.

## REVIEW mode

1. Read the review queue. Collect every row due today or earlier, most overdue first.
2. **Staleness gate, before quizzing.** If a card names a file, tool, or system, confirm
   by command that it still exists. Retired: delete the row, report `pruned: [card]`.
   Never quiz on dead infrastructure. Timeless principles stay.
3. One question per due concept, tied to something the learner built or discussed, never
   a definition prompt:

```
SRS: [concept] (due [date], interval [N] days)
One question: [concrete, tied to recent work]
Answer in one or two sentences, or type /learn skip to move on.
```

4. Grade whether the answer demonstrates the principle, not whether it recites the
   definition. Pass: next review today plus double the interval, interval doubles. Fail:
   next review tomorrow, interval back to 1. `/learn skip`: unchanged, move on.
5. At interval 14 days or more with three or more passes, mark the curriculum row done.

## What bad output looks like

| Bad output | Fix |
|---|---|
| The block opens with a definition: "A webhook is an event-driven callback." | Line 2 states the problem it solves, in the session's own situation. |
| Praise or preamble: "Great learning moment, let me explain the history." | Six lines, no wrapper. The block is not a section of the deliverable. |
| `Connects to: distributed systems, scalability`, neither in the curriculum. | Pull both names from the curriculum file, or write "new branch". |
| The block fires on a rename, or twice on the same concept. | Check the not-a-moment list and the session log first. |
| A write is claimed but the path came from nowhere. | No local context, no writes. Emit the block, say the writes were skipped. |

## Verification

Run these before returning to the session. A failure is a fix, not a note.

1. `awk '/💡 LEARN:/{c=1} c&&NF{n++} END{print n}'` over the block prints 6.
2. `grep -nP '[\x{2014}\x{2013}\x{2192}]'` over the block returns nothing.
3. Every name after `Connects to:` greps clean in the curriculum.
4. The concept appears once in the review queue; the session log gained one line.
5. Nothing follows the sign-off gate block.
6. REVIEW only: every row touched has a new date and interval, or was pruned with a
   reason.

## Changelog

- 2026-08-28 v1.3: rebuilt against the skill-rebuild bar. Two contracted modes replace a
  numbered walkthrough whose Step 0 sat after Step 1. Plan first, anti-patterns, and
  Verification added, the last being the first mechanical gate this skill has carried.
  Privacy split: the learner, the persona names, and every path moved to
  `references/local-context.md`; the skill degrades to block-only without it. The block
  shape, the six-line rule, the placement rule, `/learn srs`, `/learn skip`, and the
  handoff to `decoder` are unchanged.
- 2026-08-01 v1.2: the five-line rule was made explicit as five after the header, six
  including it, because agents were dropping a line to make the count work.
