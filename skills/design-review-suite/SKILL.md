---
name: design-review-suite
description: Review, measure, and fix a user interface against published criteria, so every finding cites a rule instead of an opinion. Use for "review my UI", "design review", "critique this screen", "check accessibility", "audit this design", "something looks off", "pre-launch review", "fix the typography", "font pairing", "add a micro-interaction", "pick a colour palette". Five modes. CRITIQUE scores usability heuristics. AUDIT measures code and rendered values into a findings table. POLISH runs the last fix pass over spacing, type, state, and motion. BUILD-CHECK gates a build against a fifteen line checklist by command. DESIGN-SYSTEM picks styles, palettes, and font pairings for new work. Every finding carries a WCAG 2.2 or Nielsen criterion, or is labelled TASTE and ranked below. Do not use for writing product copy, backend or API review, general code review, brand identity, or logo design.
---

# Design Review Suite

## Plan first

1. Restate the done condition in one line: what ships, and what proves it is ready.
2. Number the steps and name the artifact each produces.
3. Name the riskiest step and the command that checks it.
4. Pick ONE mode, state it, then execute, marking each step done or blocked.

Skipping the plan is a defect, not a shortcut.

## Read first

Read `references/standards.md` before any mode. It carries the Nielsen heuristics, the
WCAG 2.2 AA criteria with URLs, Apple and Material target sizes, the data-table rules, and
the fifteen line checklist. Read `references/local-context.md` if it exists: it supplies
the owner taste layer. Without it the skill still runs, the published criteria are the
whole standard, and the five taste-dependent checklist lines report
`SKIP, no local taste file` instead of failing.

Local-first is a hard gate on any fix work: build, run the dev server, verify on
localhost, then PR.

## Modes

Pick one. State it in the first line of output.

| Mode | Triggers | Inputs | Output | Done when |
|---|---|---|---|---|
| **CRITIQUE** | "critique this screen", "design review", "UX feedback" | live URL or screens, stated audience | heuristics table, ranked top 3, then the rest | every finding cites a criterion or is labelled TASTE |
| **AUDIT** | "check accessibility", "audit this design", "technical quality review" | source paths and a running page | findings table with measured values | zero rows with an estimated measurement |
| **POLISH** | "something looks off", "finishing touches", "fix the typography", "add a micro-interaction" | source paths, the design system | diff plus a before and after value per fix | BUILD-CHECK passes on the changed screens |
| **BUILD-CHECK** | "pre-launch review", "is this ready to ship" | running page, stated viewport | fifteen lines, PASS, FAIL, or SKIP each | verdict line printed, zero FAIL |
| **DESIGN-SYSTEM** | "pick a palette", "font pairing", new UI with no system yet | product type and industry | style, palette, and pairing with rationale | choice passes AUDIT contrast before use |

CRITIQUE judges. AUDIT measures. POLISH changes code. BUILD-CHECK gates. DESIGN-SYSTEM
generates. If two apply, run the earlier one first.

## Finding format, every mode

```
[P0-P3] <criterion> | <element or file:line> | measured <value> | required <value> | <fix>
```

`<criterion>` is a WCAG 2.2 number such as `WCAG 2.2 1.4.3`, a Nielsen heuristic number
such as `Nielsen 4`, a platform rule such as `HIG targets`, or the literal word `TASTE`.
A TASTE finding ranks below every criterion-backed finding in the same severity band.
A finding with neither a criterion nor a TASTE label does not ship: delete it or measure it.

## CRITIQUE mode

1. State the audience and the job the screen must do. Ask if not given.
2. Score Nielsen 1 to 10, zero to four each, total out of forty. Each score names the
   element that earned it. Most working interfaces land between 20 and 32.
3. Anti-pattern verdict first: would a reader believe a machine generated this, and why.
4. Rank the top 3 issues by cost to the user, not by ease of fix. Then the remainder.
5. Close with 2 to 4 questions about intent that the findings actually raised.

Playbook: `references/critique/SKILL.md`, with scoring, personas, and cognitive load in
`references/critique/reference/`. Hard stop: a critique with more than ten items and no
ranked top 3 is not deliverable.

## AUDIT mode

Measure, do not fix. Every value comes from a command, the DOM, or a screenshot.

1. Read the source. Name the files.
2. Run the rendered-page probe in `references/build-check.md` section A for contrast,
   target size, font families, and reflow.
3. Emit one table: severity, criterion, element, measured value, required value, fix.
4. Add a systemic-pattern section: which findings are one bug at a shared call site.
5. Optional rule source, per `references/web-design-guidelines/SKILL.md`: fetch
   `https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/command.md`
   fresh, never from memory, and fold its rules into the same table.

Playbook: `references/audit/SKILL.md`. Hard stop: a row whose measured value was estimated
rather than computed. Delete the row or measure it.

## POLISH mode

Never first. Do not polish incomplete work. Discover the design system before touching
anything: tokens, spacing scale, component conventions. Polish aligns to the system, and a
system that is wrong everywhere is one fix, not fifty.

Three dimension passes, each with a measured before and after:

- **Spacing and state.** Spacing-scale adherence, and all eight interaction states:
  default, hover, focus, active, disabled, loading, error, success. A missing state is
  broken behaviour, not a nit. Playbook: `references/polish/SKILL.md`.
- **Type.** Read the actual font stack from the code and quote it before advising. Modular
  scale, about five sizes, 45 to 75 characters per line, body at least 16px in rem.
  Playbook: `references/typeset/SKILL.md`.
- **Motion.** One hero moment, plus feedback, transition, and delight layers. Every
  animation names a duration and an easing token or it does not ship. Transform and
  opacity only. Bounce and elastic are banned. The `prefers-reduced-motion` block is
  mandatory. Playbook: `references/animate/SKILL.md`.

Hard stop: run BUILD-CHECK on the changed screens and paste the result.

## BUILD-CHECK mode

Run the fifteen line checklist from `references/standards.md` section 6 using the commands
in `references/build-check.md`. Print one line per item in checklist order:
number, PASS or FAIL or SKIP, the item, and the measured value.

A line reports PASS only when a command produced the value. A line you could not run
reports `SKIP, reason`. End with `VERDICT: SHIP or BLOCK, n FAIL, n SKIP`. One FAIL blocks.

## DESIGN-SYSTEM mode

Searchable database of styles, palettes, font pairings, product types, UX guidelines, and
chart types. Start every run with this, from the skill directory:

```bash
python3 references/ui-ux-pro-max/scripts/search.py "<product industry keywords>" \
  --design-system [-p "Name"] [--persist] [--page "dashboard"]
```

`--persist` writes `design-system/MASTER.md` plus per-page overrides, where the page file
beats the master. Deep dives: `--domain product|style|typography|color|landing|chart|ux`.
Playbook: `references/ui-ux-pro-max/SKILL.md`. Hard stop: run the chosen palette through
the contrast probe before any code uses it.

## What bad output looks like

1. **"Looks good to me" with no measurement.** Fix: every claim carries a number from a
   command, or the word SKIP.
2. **Gradients, shadows, or emoji offered as polish.** These are decoration, not a fix for
   a named problem. Fix: name the criterion the change satisfies, or do not make it.
3. **Twenty nits and no ranked top 3.** The reader cannot start. Fix: rank by cost to the
   user and cut the tail into one collapsed list.
4. **Typography advice without the font stack.** Advice about a font nobody is using. Fix:
   quote the computed `font-family` from the code or the DOM before advising.
5. **Motion with no duration and no easing named.** Unreviewable and unreproducible. Fix:
   state both, or drop the animation.

## Verification

- Mode named in line one, and the playbook file read is named.
- Every finding matches the finding format. Check: `grep -cE 'WCAG|Nielsen|HIG|TASTE'`
  against the finding count. They must be equal.
- Scores trace to specific elements. Summary counts match the listed items.
- AUDIT and BUILD-CHECK: each measured value names the command that produced it.
- POLISH: localhost verified, BUILD-CHECK output pasted, before and after values shown.
- Banned characters in anything this skill writes, portable on BSD and GNU:
  `python3 -c "import sys;[print(i,l) for i,l in enumerate(open(sys.argv[1]),1) if set(l)&set(chr(8212)+chr(8211)+chr(8594))]" FILE`
  prints nothing.

## Changelog

- [2026-07-02] Suite created. Absorbed critique, audit, polish, typeset, animate,
  ui-ux-pro-max, and web-design-guidelines. Full playbooks copied to `references/`.
- [2026-08-28] Rebuild to sellable standard. Seven modes collapsed to five: TYPESET and
  ANIMATE fold into POLISH as dimension passes sharing its procedure, WEB-GUIDELINES folds
  into AUDIT as an optional rule source. Added `references/standards.md` as the mandatory
  first read, a criterion-citing finding format, BUILD-CHECK with a verified rendered-page
  probe in `references/build-check.md`, and five anti-patterns. Owner taste moved to
  `references/local-context.md` under the two-layer privacy split.
