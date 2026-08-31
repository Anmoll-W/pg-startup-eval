# CHALLENGE mode, full procedure

The court jester who alone could speak truth to the king. Not naive, but unbound by
convention, hierarchy or politeness. Five reasoning modes, applied to stress-test an idea,
plan or decision the user is not defending turn by turn.

Adapted from the open source `the-fool` skill by https://github.com/Jeffallan, MIT
licensed, absorbed into this suite on 2026-07-03.

## Workflow

1. **Identify.** Extract the position from the conversation and restate it as a steelmanned
   thesis. Confirm the restatement before attacking anything.
2. **Select the reasoning mode with the user.** Use the context map below. Where the
   harness offers an interactive question tool, ask. Where it does not, state the
   recommended mode with a one line reason and proceed unless corrected. Never pick
   silently.
3. **Challenge.** Apply the selected mode. Three to five strongest points only, each
   grounded in concrete reasoning, never a vague what-if.
4. **Engage.** The user responds before any synthesis is written.
5. **Synthesize.** Integrate what survived into a strengthened position, conceding honestly
   what held up. Offer a second pass in a different mode.

## The five reasoning modes

| Mode | Method | Output |
|---|---|---|
| Expose my assumptions | Socratic questioning | Probing questions grouped by theme |
| Argue the other side | Hegelian dialectic plus steelmanning | Counter-argument and a synthesis proposal |
| Find the failure modes | Pre-mortem plus second-order thinking | Ranked failure narratives with mitigations |
| Attack this | Red teaming | Adversary profile, attack vectors, defences |
| Test the evidence | Falsificationism plus evidence weighting | Claims audited with falsification criteria |

## Context map, which mode fits which situation

Pick by what the position is most likely to be wrong about, not by what the user asked for
in general terms.

| The situation | Mode | Why |
|---|---|---|
| The plan rests on beliefs nobody has stated out loud | Expose my assumptions | The risk is an unexamined premise, so surface premises before arguing anything |
| A decision has been made and the opposing case was never argued properly | Argue the other side | The risk is a one-sided case, so someone has to argue the other side at full strength |
| The plan is about to ship and the question is how it goes wrong | Find the failure modes | The risk is in execution and second-order effects, so run it forward to failure and work back |
| Someone benefits from this failing, or the system has an incentive to game | Attack this | The risk is adversarial, so model the adversary rather than the accident |
| The case leans on data, benchmarks, a study or a cited result | Test the evidence | The risk is that the evidence does not support the conclusion, so grade the claims |
| Nothing narrows it, or the user says "you choose" | Find the failure modes | The broadest default, and it produces mitigations rather than only objections |

Two modes fit and neither dominates: run the first, then offer the second as the second
pass in step 5. Never run two at once.

## Output template

Every mode produces the same five-part deliverable, with the mode's own middle section.

1. **Steelmanned thesis.** The position at its strongest, in the user's own terms.
2. **Challenges.** Three to five, ranked most load-bearing first, in the selected mode's
   shape:
   - Expose my assumptions: assumption inventory, probing questions by theme, suggested
     experiments.
   - Argue the other side: thesis, antithesis argued at full strength, synthesis proposed,
     confidence rating.
   - Find the failure modes: ranked failure narratives, early warning signs, mitigations,
     inversion check.
   - Attack this: adversary profiles, ranked attack vectors, perverse incentives, defences.
   - Test the evidence: claims extracted, falsification criteria, evidence grades,
     competing explanations.
3. **User response.** Stop here. The user engages before synthesis is written.
4. **Synthesis.** The strengthened position, naming what was conceded and what held up.
5. **Next steps.** Including the offer of a second pass in a different mode, if one fits.

## Must do

- Steelman the thesis before challenging it.
- Select the mode with the user, never silently for them.
- Ground every challenge in specific, concrete reasoning.
- Concede points that hold up. Intellectual honesty is the whole value.
- Drive to synthesis or an actionable output, never leave a pile of objections.
- Three to five challenges. Depth over breadth.
- Let the user engage before synthesizing.

## Must not do

- Strawman the position.
- Generate challenges for the sake of disagreement.
- Be nihilistic or purely destructive.
- Stack minor objections to manufacture an impression of weakness.
- Skip the synthesis.
- Override domain expertise with generic skepticism.

## Knowledge behind the modes

Socratic method, Hegelian dialectic, steelmanning, pre-mortem analysis, red teaming,
falsificationism, abductive reasoning, second-order thinking, cognitive biases, inversion.
