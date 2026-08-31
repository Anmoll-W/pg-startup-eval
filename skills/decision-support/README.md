# Decision Support

*A skill by [The PM Code](https://www.linkedin.com/company/the-pm-code/). Follow us on LinkedIn.*

---

You have an idea. It feels good. It has felt good for a week, which is exactly the problem, because nothing has pushed on it yet. The people around you are being kind. Kindness is not evidence.

Decision Support is a Claude Code skill that pushes on a decision before you commit to it. It runs in one of four modes, and it names the mode before it says anything else, so you always know which job is running.

---

## Four modes

**EVALUATE** judges an idea, a startup, or a side project and ends with a verdict that does not hedge. It pulls live market research first, sizes the market from the bottom up, scores ten blocks, names the three fatal flaws, and lands on one of `Strong`, `Weak`, or `Pivot required`. Then it writes a kill criterion: the single line that says what would end this idea, and when to look. A verdict with nothing that could contradict it is not a verdict, so this mode refuses to give one without the kill line.

**GRILL** interviews you, one question at a time, as the CTO you will have to answer to three months from now. No "and also" questions. No generic "have you thought about edge cases", because it names the edge case instead. Every time you say "we will figure that out later", that phrase goes on the open list by name. It ends with a written artifact: what is resolved, what is still open and why each open item matters, and the next steps ranked by how load-bearing they are.

**INVERT** takes a solution someone has already proposed and runs it back to the problem it claims to solve. It reads the solution as evidence a problem might exist, never as a spec to build. Then it grades the evidence twice, on purpose, because one grade hides the gap: does the pain actually exist and for whom, and separately, has the causal story ever been tested. A tested fix aimed at a problem nobody has is still nothing.

**CHALLENGE** attacks a position you are not defending turn by turn. It steelmans your position first and confirms the steelman before it lays a finger on it, picks a reasoning mode, raises three to five challenges, then synthesises, conceding what held up. It will not hand you a pile of eleven objections and walk away.

---

## What it will not do

Written into the skill, not left to mood:

- No cheerleading. Enthusiasm is not evidence, and agreement is not a service.
- No verdict, grade, or recommendation without the evidence stated underneath it.
- No market claim without a bottom-up number, or an explicit "not sized".
- No verdict without a kill criterion.
- Never more than one question per turn in GRILL.
- No invented number, ticket, count, or source to make an output look concrete.

---

## The double grade, and why it exists

The sharpest thing this skill does is refuse to build for you.

INVERT grades problem evidence and mechanism evidence separately, each as `real`, `partial`, or `none`, and the pair decides the call. Problem `none` means kill it or make it a research task, never a build. Mechanism `none` means park it as a hypothesis with the test that would settle it. Both `real` means build, and name the metric that would show the mechanism failing here.

This is not theoretical. The mode once looked at a proposal to move one of its own author's tools to a different folder and recommended deleting the tool instead. The pain was real enough, but the fix had never been tested, and a confirmed pain with an untested fix is a candidate, not a build. It said so, and it was right.

---

## Install

```bash
git clone https://github.com/Anmoll-W/thepmcode-skills
cp -r thepmcode-skills/skills/decision-support ~/.claude/skills/decision-support
```

Once installed, it activates inside Claude Code when you ask to evaluate an idea, stress-test a plan, run a pre-mortem, or decide whether to build something. Say "grill me on this plan" or "evaluate this idea" and it picks the mode.

---

## Built for

Product people who would rather be told the truth now than discover it after a quarter of build. Founders who are tired of feedback that makes them feel good and teaches them nothing. Anyone who has ever shipped the thing everyone agreed with and watched it fail.

---

MIT licensed. See [LICENSE](../../LICENSE).

*Built by [The PM Code](https://www.linkedin.com/company/the-pm-code/).*
