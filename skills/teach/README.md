# Teach

*A skill by [The PM Code](https://www.linkedin.com/company/the-pm-code/). Follow us on LinkedIn.*

---

You just made a real decision. You chose a metric over a vanity number, or you argued build against buy and won, or your engineer taught you why the webhook needed a queue. It was a genuine lesson. Then the session ended, the next one started, and it was gone.

Teach is a Claude Code skill that catches that lesson without breaking the session it came from. When real work produces something worth keeping, it writes six lines, logs the concept, and schedules it to come back. It is small on purpose. A lesson that costs the session its flow is not read twice.

---

## Two modes

**INJECT** fires on its own the moment a session produces something teachable: an architectural decision with its reason on the record, a named pattern applied, a product judgment call, a book or case study cited, a metric analysed. It does not fire on a rename, a reformat, or a concept it already logged this session. When it fires, it emits one block:

```
💡 LEARN: [Cluster N: exact skill name | General: concept name]
[One sentence: the problem this exists to solve, before any definition]
[One sentence, two at most: the underlying principle or trade-off]
[One sentence: where this shows up in your work]
Connects to: [1 or 2 concepts already in your curriculum, or "new branch"]
Say "teach me [skill name]" for the full breakdown
```

Then it marks the concept in a curriculum file and seeds it into a spaced-repetition queue due tomorrow.

**REVIEW** runs when you ask for it. It reads the queue, collects everything due, and asks one question per concept, tied to something you actually built, never a definition prompt. Pass, and the interval doubles. Fail, and it resets to tomorrow.

---

## The rules that keep it small and true

- **Six lines, no wrapper.** Exactly five lines after the header. No preamble, no "great learning moment", no history lesson.
- **Line two opens with the problem, never the definition.** "We used a webhook because polling wasted requests on a quiet stream" beats "a webhook is an event-driven callback."
- **`Connects to:` names concepts that exist.** It pulls the names from your curriculum file. An invented link is worse than "new branch", because it makes the map of what you know unfalsifiable.
- **One block per session, never the same concept twice.**
- **It never claims a write it did not make.** With no local context to write into, it emits the block, uses a general cluster, and says the writes were skipped rather than inventing a path.

---

## The staleness gate

The review mode has one rule most spaced-repetition tools miss. Before it quizzes you on a card that names a file, a tool, or a system, it confirms by command that the thing still exists. If you retired that infrastructure, the card is deleted and reported as pruned. You are never quizzed on a system you tore out three weeks ago. Timeless principles stay; dead facts go.

---

## Install

```bash
git clone https://github.com/Anmoll-W/thepmcode-skills
cp -r thepmcode-skills/skills/teach ~/.claude/skills/teach
```

Once installed, INJECT fires on its own inside Claude Code when a session earns a lesson. Say "run my SRS review" or "quiz me on what I learned" to trigger REVIEW.

---

## Built for

People who learn by shipping and keep re-learning the same thing because nothing held it in place. This skill turns the work you already do into the curriculum you never sat down to write.

---

MIT licensed. See [LICENSE](../../LICENSE).

*Built by [The PM Code](https://www.linkedin.com/company/the-pm-code/).*
