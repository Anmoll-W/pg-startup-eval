# Design Review Suite

*A skill by [The PM Code](https://www.linkedin.com/company/the-pm-code/). Follow us on LinkedIn.*

---

Someone looks at the screen and says it feels off. You agree. Neither of you can say which rule it breaks, so the conversation turns into taste versus taste, and the loudest opinion wins. That is how a screen ships with a contrast ratio that fails and a tap target a thumb keeps missing.

Design Review Suite is a Claude Code skill that turns "this looks off" into a finding with a rule number attached. Every finding cites a WCAG 2.2 criterion or a Nielsen heuristic, or it is labelled TASTE and ranked below everything that is not. It runs in one of five modes, named in the first line of output.

---

## Five modes

| Mode | You ask for | What it does |
|---|---|---|
| **CRITIQUE** | "critique this screen", "UX feedback" | Scores the Nielsen heuristics against named elements, ranks the top three by cost to the user |
| **AUDIT** | "check accessibility", "audit this design" | Measures contrast, target size, font stacks, and reflow into a table where every value came from a command |
| **POLISH** | "something looks off", "fix the typography" | Runs the last pass over spacing, state, type, and motion, with a before and after value per fix |
| **BUILD-CHECK** | "pre-launch review", "is this ready" | Reads a fifteen-line checklist by command and prints one verdict |
| **DESIGN-SYSTEM** | "pick a palette", "font pairing" | Chooses styles, palettes, and pairings, then runs them through the contrast probe before any code uses them |

CRITIQUE judges. AUDIT measures. POLISH changes code. BUILD-CHECK gates. DESIGN-SYSTEM generates. If two apply, it runs the earlier one first.

---

## The finding format

```
[P0-P3] <criterion> | <element or file:line> | measured <value> | required <value> | <fix>
```

The criterion is a WCAG 2.2 number, a Nielsen heuristic number, a platform target-size rule, or the literal word TASTE. A finding with neither a criterion nor a TASTE label does not ship: it gets deleted or measured. A TASTE finding always ranks below a criterion-backed finding in the same severity band, so a subjective preference can never outrank a real accessibility failure.

---

## The rules that make it honest

- **AUDIT measures, it does not estimate.** A row whose value was guessed rather than computed does not ship. Delete it or measure it. Every value names the command, the DOM read, or the screenshot it came from.
- **POLISH is never first.** It refuses to polish incomplete work, and it discovers the design system before touching anything, because a system that is wrong everywhere is one fix, not fifty. Then it gates itself: it runs BUILD-CHECK on the changed screens and pastes the result.
- **Motion names its numbers.** Every animation states a duration and an easing token or it does not ship. Transform and opacity only. Bounce and elastic are banned. The reduced-motion block is mandatory.
- **Typography quotes the real font stack** from the code before it advises, so you never get advice about a font nobody is using.
- **BUILD-CHECK is a command gate.** A line reports PASS only when a command produced the value. A line it could not run reports SKIP with a reason. One FAIL blocks the ship.

---

## Built from seven, collapsed into five

This suite absorbed seven smaller tools: critique, audit, polish, typeset, animate, a UI pattern database, and a web guidelines reference. The rebuild folded typeset and animate into POLISH as dimension passes, folded the guidelines into AUDIT as an optional rule source, and put a mandatory first read at the front, `references/standards.md`, that carries the Nielsen heuristics, the WCAG 2.2 criteria with their URLs, the platform target sizes, and the fifteen-line checklist. The result is one finding format and one verification section, so a subjective critique and a measured audit come out speaking the same language.

Two of the reference folders are not original. DESIGN-SYSTEM reads the MIT-licensed ui-ux-pro-max pattern database, and AUDIT can fold in the MIT-licensed Vercel Labs web interface guidelines. Both keep their own license, credited in [NOTICE.md](NOTICE.md).

---

## Install

```bash
git clone https://github.com/Anmoll-W/thepmcode-skills
cp -r thepmcode-skills/skills/design-review-suite ~/.claude/skills/design-review-suite
```

Once installed, it activates inside Claude Code when you ask for a design review, an accessibility check, a polish pass, a pre-launch review, or a palette and font pairing.

---

MIT licensed for the original work. See [LICENSE](../../LICENSE) and [NOTICE.md](NOTICE.md).

*Built by [The PM Code](https://www.linkedin.com/company/the-pm-code/).*
