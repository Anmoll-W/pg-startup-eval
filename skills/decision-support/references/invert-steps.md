# INVERT, the seven steps in full

`SKILL.md` carries the contract, the evidence-grade rule and the hard stops. This file is
the long form of each step. If it is absent, the contract in `SKILL.md` is complete on its
own: run the seven steps as written there.

Use INVERT when someone hands over a solution ("we need X", "let us build Y") and the
underlying problem needs checking before anyone commits, or when triaging a backlog of your
own ideas. Two directions, same seven steps: forward for someone else's proposed solution,
reverse for your own idea fed in the same way.

## 1. Take the solution as evidence, not a spec

Restate it in one line. Name the likely signal that produced it: a support pattern, a
competitor move, a personal frustration. If a project is named and you have file access,
read its decision log, hypothesis list and support-data file (paths in `local-context.md`)
before writing anything. A prior finding on this exact question outranks fresh reasoning.
If you cannot read them, say so in one line and continue. Never state what those files say
without having read them.

## 2. Decompress to the underlying problem

One sentence: who is stuck, on what, and what it costs them in trust, time, money or
retention. Ground it in real data from a system the environment actually has. No data
found: label the problem statement `unverified` and carry that label through steps 5 and 6.
Still complete every step. Never let an unverified problem be recommended as if it were
confirmed. A sentence containing a product noun is the solution wearing a problem costume,
so rewrite it.

## 3. List three to five assumptions baked into the proposed solution

Each with the risk if it is wrong, and one check a human could run this week, naming the
system and the query ("support tool: tickets tagged billing, last 50", "analytics: exit
rate on the pricing page, 28 days"). Never "do more research". These rows are recommended
actions, not results: never invent a ticket ID, a count or a finding to make a row look
concrete.

## 4. Generate three alternative framings of the same underlying problem

Each has to point at a genuinely different solution space. If all three collapse into
variations of the same build, the problem statement in step 2 is still too solution-shaped:
redo step 2 once. If the second attempt still collapses, stop and say so. A problem that
genuinely admits one solution space is itself a finding. Never invent a third framing to
fill the slot.

## 5. Grade evidence twice, separately, because a single grade hides the gap

**Problem evidence:** does the pain actually exist, and for whom. **Mechanism evidence:**
has the proposed solution's causal story, that this change moves that behaviour, been
tested anywhere. Each grade is `real`, `partial` or `none`. Read the pair:

- Problem `none`: kill it, or convert it into a research task. Never a build, whatever the
  mechanism grade. A tested mechanism aimed at a problem nobody has is still nothing.
- Problem `real` or `partial`, mechanism `none`: the pain is confirmed and the fix is still
  a guess. Park it as a candidate hypothesis with the test that would settle it. Do not build.
- Problem `real` or `partial`, mechanism `partial`: build only the smallest slice that would
  falsify the causal story, not the full solution.
- Problem `real`, mechanism `real`: build it, and name the metric that would tell you the
  mechanism failed in this specific context.

State both grades in words. Never blend them into one verdict, and never imply one.

## 6. Recommend

Pick one framing, or explicitly kill the idea, and say why in one line, tied to the evidence
pair from step 5. One recommendation, never a menu of options to choose between.

## 7. Draft the message

Two to three sentences the original proposer can read without feeling blocked: what problem
you are chasing on their behalf, what you found, and what you propose instead, or a
confirmation that they were right.
