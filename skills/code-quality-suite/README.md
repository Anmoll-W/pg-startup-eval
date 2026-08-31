# Code Quality Suite

*A skill by [The PM Code](https://www.linkedin.com/company/the-pm-code/). Follow us on LinkedIn.*

---

The branch is done. It works on your machine. Someone is about to approve it, and the honest truth is that nobody has actually looked for the bug yet. Everyone read the diff. Reading a diff is not finding a bug.

Code Quality Suite is a Claude Code skill that looks for the bug before it ships, and refuses to tell you the code is fine without pasting the test output that says so. It runs in one of five modes. You pick one, it states it, it runs it.

---

## Five modes

| Mode | You ask for | You get back |
|---|---|---|
| **FIND-BUGS** | "find bugs", "review this branch" | Ranked findings, each with a reproduction |
| **SECURITY** | "security review", "OWASP review" | Findings scoped to the OWASP Top 10, each with a category code |
| **QA-CHECKLIST** | "QA checklist", "test plan" | A test plan built from the code, eight categories per feature |
| **WEBAPP-TEST** | "test this web app" | A Playwright run with the console output pasted |
| **PRE-LAUNCH** | "pre-launch audit" | A whole-repo audit with an independent verification pass |

---

## Every finding has the same shape

No prose. No fifteen unranked nits. Every finding, in every mode, comes out like this:

```
[SEVERITY] Title
File:line      path/to/file.ts:42
Trigger        the input or state that makes it fail
Wrong output   what happens instead
Fix            the change to make, one or two lines
Test           the test and assertion that fails before the fix
```

Severity is Blocker, High, Medium, or Low. A finding with no reproduction is not a Blocker. It gets the label `SUSPECTED` and ranks last, always. Correctness ranks before style, so the suite will not open a paragraph of spacing nits while a Blocker is sitting there unfixed.

---

## The rules that make it trustworthy

Written into the skill, not left to the reviewer's mood:

- **No "looks fine" without pasted test output.** A verdict with no command behind it is not a verdict.
- **No finding without `file:line` and a reproduction**, unless it is labelled `SUSPECTED` and ranked last.
- **SECURITY reports only a confirmed pattern with an attacker-controlled input.** A concatenation with an untraced source is filed `SUSPECTED`, not flagged as a hole. It traces the tainted value to its origin first.
- **No rewriting your code unasked.** A finding names the fix. You write it.
- **PRE-LAUNCH never lets a specialist be the last word on its own claim.** After six specialists run in parallel, a separate agent runs whose only job is to confirm, downgrade, or reject each finding. The suite reports the pass rate and the blockers, each with a one-line reason it would ship broken.

---

## Built from five, hardened into one

This suite started as five separate skills: find-bugs, security-review, a QA checklist generator, a webapp tester, and a pre-launch auditor. They shared nothing, so a finding from one looked nothing like a finding from another, and a subagent with no session history could not run any of them reliably.

The rebuild fixed that. One baseline that every mode runs by command. One finding format. OWASP category codes and a stated ASVS bar on the security side. An inputs block that a context-free subagent has to print before it reviews a single line, so it can never review a file it did not open. The verification section at the bottom is mechanical: it lists the commands that prove the run happened, and a grep that fails the run if a banned character slipped in.

Two of the modes read bundled reference material that is not original. SECURITY reads from the OWASP Cheat Sheet Series, and WEBAPP-TEST reads a Playwright driver reference. Both keep their own license, credited in [NOTICE.md](NOTICE.md).

---

## Install

```bash
git clone https://github.com/Anmoll-W/thepmcode-skills
cp -r thepmcode-skills/skills/code-quality-suite ~/.claude/skills/code-quality-suite
```

Once installed, it activates inside Claude Code when you ask to review a branch, find bugs, run a security or OWASP review, write a test plan, or run a pre-launch audit.

---

MIT licensed for the original work. See [LICENSE](../../LICENSE) and [NOTICE.md](NOTICE.md).

*Built by [The PM Code](https://www.linkedin.com/company/the-pm-code/).*
