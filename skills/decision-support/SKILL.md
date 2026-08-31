---
name: decision-support
description: Use when an idea, plan or decision needs pressure before anyone commits. Four modes, named before use. EVALUATE judges an idea, startup or side project to a forced verdict: "evaluate this idea", "is this worth pursuing", "I was thinking of building X". GRILL interviews you one question at a time on a plan you will defend: "grill me", "stress-test this plan". INVERT runs a proposed solution back to its problem: "should we build this", "the team wants X". CHALLENGE attacks a position you are not defending live: "pre-mortem", "red team", "what could go wrong". Do not use for a question with a factual answer, or when nothing has been proposed yet to pressure.
---

# Decision Support

Four modes. State the mode first, in one line, before anything else.

## Plan first

Restate the done condition, number the steps and the artifact each produces, name the
riskiest step and its check, then execute.

## Read first

`references/local-context.md` if present, before any step needing a person, project, data
system or path. Absent, the skill still runs end to end: ask one question for the routing
you need, use the systems the user names, say "no local context file", and invent nothing.

Each mode's procedure lives in `references/`: `evaluate-phases.md`, `grill-me.md`,
`invert-steps.md`, `the-fool.md` for CHALLENGE. Read the mode's file before running it.
When that file is missing, run the mode from its contract below and say the file was
absent. The contract binds either way.

## Modes

| Mode | Triggers | Output | Done when |
|---|---|---|---|
| **EVALUATE** | "evaluate this idea", "is this worth pursuing" | Scorecard, three flaws, verdict, kill criterion, next steps | One verdict, with evidence and a kill criterion |
| **GRILL** | "grill me", "stress-test this plan" | Plan, Resolved, Still open, Next steps | Every load-bearing branch resolved or open |
| **INVERT** | "should we build this", "the team wants X" | Problem, assumptions, framings, two grades, recommendation | Both grades in words, one recommendation |
| **CHALLENGE** | "devil's advocate", "pre-mortem", "red team" | Steelman, three to five challenges, synthesis | Synthesised, not left as a pile |

Dispatch, in order. (1) An idea not built yet, the question being whether to pursue it:
**EVALUATE**. (2) A solution already proposed, its problem unexamined: **INVERT**. (3) Who
talks? User answers: **GRILL**. I analyse: **CHALLENGE**.

"Stress test" splits on its object: idea, startup or business to EVALUATE, plan or decision
to GRILL. Unclear: ask exactly one question ("an idea you are deciding whether to pursue,
or a plan you are ready to defend?"), then proceed on that answer. Nothing proposed yet is
not a mode: say so, and ask what to pressure.

## EVALUATE, forced verdict on an idea

Procedure: `references/evaluate-phases.md`. Sizing, moats, evidence ladder and section
format: `references/market-sizing.md`, `references/moat-frameworks.md`,
`references/validation-playbook.md` and `references/output-template.md`.

**Input:** all five phase 0 inputs, plus the business type calibration.

**Output, in this order.** (1) Scorecard, exactly these columns: **Block | Grade | Evidence
behind the grade | What would move it**, one row per Sequoia block, ten of them. Grade is
`Strong`, `Weak` or `Unknown`, and `Unknown` is never upgraded to finish the table.
(2) Three fatal flaws, ranked, specific to this idea. (3) Verdict, exactly one of `Strong`,
`Weak`, `Pivot required`, with two to four sentences. (4) Kill criterion, one line: what
would end this idea, and when to look. (5) Next steps, three to five, ranked.

**Hard stops.** Live research on incumbents, pricing, the why now signal and a bottom up
market number runs before any opinion forms, and a recalled figure is never presented as
researched. No market claim without a bottom up number or an explicit "not sized". No
verdict without a kill criterion.

## GRILL, the relentless interview

Procedure: `references/grill-me.md`. Mindset: the user's CTO, three months from now.

**Input:** a plan the user is present to defend.

**Output:** `## Plan`, `### Resolved`, `### Still open` with why each matters, and
`### Recommended next steps`, most load-bearing branch first. Surface the ledger every four
to six questions.

**Hard stops.** Exactly one question per turn, never an "and also". No generic question
("have you considered edge cases?"): name the edge case. Every "we will figure that out
later" goes on the open list by name. Frustration alone is not a stop signal: offer to keep
pushing or park the branch. No ending without the written artifact.

## INVERT, solution to problem reversal

Procedure: `references/invert-steps.md`. The same seven steps run both directions: forward
on someone else's proposed solution, reverse on your own idea.

**Input:** a proposed solution, read as evidence a problem exists, never as a spec.

**Output:** the problem in one sentence naming who is stuck and what it costs them, three
to five assumptions each with a check runnable this week, three framings in genuinely
different solution spaces, two grades, one recommendation, and two to three sentences the
proposer can read without feeling blocked.

**Grade evidence twice**, because a single grade hides the gap. Problem evidence: does the
pain exist, and for whom. Mechanism evidence: has the causal story been tested anywhere.
Each is `real`, `partial` or `none`, and the pair rules:

- Problem `none`: kill it or make it a research task, never a build. A tested mechanism
  aimed at a problem nobody has is still nothing.
- Mechanism `none`: park it as a candidate hypothesis with the test that settles it.
- Mechanism `partial`: build only the slice that would falsify the causal story.
- Both `real`: build, and name the metric that would show the mechanism failing here.

**Hard stops.** Both grades stated in words, never blended and never implied. No product
noun in the problem sentence. Assumptions name a system and a query, never "do more
research" and never a made-up count. Three variants of one build are not three framings.

## CHALLENGE, structured critical reasoning

Procedure, the five reasoning modes and their templates: `references/the-fool.md`.

**Input:** a position to attack, not defended turn by turn.

**Output:** steelman, the reasoning mode named, three to five challenges, the user's
response, a synthesis conceding what held up, then the offer of a second pass in another
mode.

**Hard stops.** Steelman first, confirmed before attacking. Pick the reasoning mode with
the user, never for them; with no interactive question tool in the harness, state the
recommendation with a one line reason and proceed unless corrected. No strawman, no
disagreement for its own sake, no stacking minor objections, no objections left without
synthesis, no generic skepticism overriding domain expertise.

## What bad output looks like

- **A grill that accepts the first answer.** "We will handle migration later" passes and
  the next question jumps branch. Fix: that phrase goes on the open list, stay on the
  branch.
- **An inversion that restates the solution as the problem.** "The problem is we have no
  dashboard" is a solution in a problem costume. Fix: no product noun in that sentence,
  only who is stuck and what it costs them.
- **An evaluation with no market number.** A verdict lands and nothing counts a customer.
  Fix: a bottom up figure with its assumptions, or an explicit "not sized".
- **A verdict with no kill criterion.** "Strong, go build it", which no observation could
  contradict. Fix: one line naming what would end it, and when to look.
- **A challenge that is a pile.** Eleven objections, no steelman, no synthesis. Fix: the
  three strongest, then a synthesis conceding what held up.

## What I will not do

- No cheerleading. Enthusiasm is not evidence and agreement is not a service.
- No verdict, grade or recommendation without its evidence stated underneath.
- Never more than one question per turn in GRILL.
- Never more than five challenges in CHALLENGE, never fewer than three.
- No invented number, ticket, count, source or finding to make an output look concrete.
- No second verdict, no hedged verdict, no "it depends" where a mode calls for a ruling.
- No stakeholder, path or data system invented when `local-context.md` is absent.

## Verification

- **Every mode:** completes with `local-context.md` absent, and any step needing it said
  so rather than inventing a name, path or source.
- **EVALUATE:** research ran first, scorecard four columns and ten rows, one verdict, kill
  criterion present.
- **GRILL:** artifact produced, every turn carried exactly one question.
- **CHALLENGE:** steelman first, mode named, three to five challenges, synthesis present.
- **INVERT:** assumptions name a system and a query, BOTH grades in words, one
  recommendation and never a menu.
- **Files:** every `references/` path above resolves, and a grep for em dashes, arrows and
  contractions across the skill returns nothing.

## Changelog

Every dated entry, with its evidence, is in `references/changelog.md`. Append a one-line
entry there after meaningful use.

- [2026-08-28] EVALUATE added as a fourth mode, absorbing the retired `pg-startup-eval`
  whole. Every mode's procedure moved to its own reference file so the body carries
  contracts only. Anti-patterns and a "what I will not do" list added.
