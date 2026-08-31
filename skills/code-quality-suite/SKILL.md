---
name: code-quality-suite
description: Find the bugs and security holes in a change before it ships, with a reproduction and a named test behind every finding. Use for "find bugs", "review this branch", "security review", "find vulnerabilities", "OWASP review", "QA checklist", "test plan", "pre-launch audit", "audit this repo". Five modes: FIND-BUGS (diff correctness), SECURITY (OWASP Top 10 at an ASVS Level 1 bar), QA-CHECKLIST (codebase-grounded test plan), WEBAPP-TEST (drives a local app with Playwright), PRE-LAUNCH (whole-repo audit with an independent verification pass). Report only. Do not use for writing features, style-only refactors, or performance work with no correctness question attached.
---

# Code Quality Suite

Five modes. Pick one, state it, run it.

## Plan first

1. Restate the done condition: which code, which mode, what the caller receives.
2. Number the steps, name the artifact each produces.
3. Name the riskiest step and the command that checks it.
4. Execute, marking each done or blocked. Skipping this is a defect.

## Read first

`references/standards.md`, before any mode: review scope, size band, OWASP table, ASVS baseline, test expectation, checklist. Then `references/local-context.md` if present: local tripwires, save paths, agent routing. Absent, the suite runs unchanged, items 6 to 12 are skipped, and the report says "no local tripwire file found" rather than inventing rules.

## Inputs, stated first

You may be a subagent with no session history. Assume nothing, print first: **target** (diff range, branch, pull request, or path), **repo root** (absolute, `git rev-parse --show-toplevel`), **test command** (exact; if none, say so and no mode returns a passing verdict). Mark what you derived. Never review a file you did not open in this run.

## Modes

| Mode | Triggers | Inputs | Output | Done when | Playbook |
|---|---|---|---|---|---|
| FIND-BUGS | "find bugs", "review this branch" | target, root, tests | ranked findings | files read, audit printed | `references/find-bugs/SKILL.md` |
| SECURITY | "security review", "OWASP" | target, root, stack | findings, OWASP codes | inputs traced to source | `references/security-review/SKILL.md` |
| QA-CHECKLIST | "QA checklist", "test plan" | feature path, spec | checklist file | eight categories per feature | `references/qa-checklist.md` |
| WEBAPP-TEST | "test this web app" | URL or start command | script, run output | flow run, evidence pasted | `references/webapp-testing/SKILL.md` |
| PRE-LAUNCH | "pre-launch audit" | repo path or URL | ranked report | verified, pass rate stated | `references/pre-launch-audit.md` |

## The baseline, run by every mode

Run these, paste the output. A claim with no command output is not a check.

1. **Tests:** the stated command, tail pasted, pass and fail counts.
2. **Diff size:** `git diff --stat <range>`. Near 100 lines is the band, detection drops past 400 (standards.md section 1). Past that, review in parts and name the part.
3. **Secrets:** `grep -rniE "(api[_-]?key|secret|password|token)\s*=\s*['\"]" <changed files>`.
4. **Markers:** `grep -rn "TODO\|FIXME" <changed files>`, an unlinked marker is a finding.
5. **Migrations:** `git diff --name-only <base> -- '*migration*'`, an edited file is a blocker.
6. **Fencing:** `grep -rn "external_content" <files>` where scraped text enters a prompt.
7. **Tripwires:** run the table in local-context.md, each marked pass, fail, or n/a.

## Finding format, every mode

```
[SEVERITY] Title
File:line      path/to/file.ts:42
Trigger        input or state that makes it fail
Wrong output   what happens instead
Fix            the change to make, one or two lines
Test           the test and assertion that fails before the fix
```

Severity: Blocker, High, Medium, Low. No reproduction means the label `SUSPECTED`, ranked last, never a blocker. Correctness ranks before style.

## FIND-BUGS mode

1. Read every changed file end to end. Diff truncated: open the files.
2. Map the failure surface per file: user input, queries, auth checks, session writes, external calls, money paths, concurrency.
3. Walk each file against the list: injection, escaping, authentication, object ownership, cross-site request forgery, races, session expiry, secrets, disclosure, unbounded work, business-logic edges (empty, boundary, overflow, retry, double submit).
4. Check each candidate against surrounding code: handled upstream, tested already.
5. Print the pre-conclusion audit: files read in full, list coverage, what you could not verify.

No verdict without step 5 and the baseline test output.

## SECURITY mode

The FIND-BUGS spine, scoped to the OWASP Top 10 (standards.md section 2). Load the matching topic, language, and infrastructure guides under `references/security-review/` first.

1. Research the whole repository even when the report covers one diff: trace tainted values to source first.
2. Report only when the vulnerable pattern and an attacker-controlled input are both confirmed. Untraced: `SUSPECTED`, ranked last. Theoretical: unreported.
3. Cite the OWASP category per finding, for example `A03 Injection`.
4. Skip test files, dead code, server-controlled config, framework escaping in force. Flag the escape hatches: `|safe`, `mark_safe`, `dangerouslySetInnerHTML`, `v-html`, raw SQL interpolation. Always flag evaluated user input, unsafe deserialization, shell execution on user input, string-built SQL, hardcoded secrets.
5. State the bar. Default ASVS Level 1: easily discovered Top 10 flaws, testable from outside. Level 2 adds per-function access-control proof, session lifecycle and re-authentication, positive-schema validation, key management, and log hygiene, which need source access and a threat model.

## QA-CHECKLIST mode

Never from memory. Read the source first: every screen, component, API call, auth boundary, acceptance criterion. Group by feature, one item per line as `- [ ] test, expected result`, across eight categories: happy paths, edges and errors, auth and session, API failures and loading, navigation and deep links, offline, performance, platform and accessibility. Name the edge cases, a heading with no case under it is not coverage. Save to the local-context.md path, else `docs/qa-checklist.md`. After a run: `[x]` pass, `[!]` fail with repro, `[-]` not applicable.

## WEBAPP-TEST mode

Native Python Playwright, sync API, headless Chromium. Static HTML: read the file for selectors. No server up: `python references/webapp-testing/scripts/with_server.py --server "<start command>" --port <port> -- python automation.py`. Server up: navigate, `page.wait_for_load_state('networkidle')` before DOM inspection, act on the selectors found, prefer `text=` and `role=`, close the browser, paste console errors and output.

## PRE-LAUNCH mode

Read only, whole repository.

1. Locate or clone the repo, build a recon brief: tree, manifest, config, routes, migrations, line count, tests, CI, env example.
2. Dispatch six specialists in one message, in parallel: security and auth, performance, database, architecture, UX with accessibility and SEO, deployment and dependencies. Each prompt carries the repo path, the brief, its scope, the finding format above, and the hard rules verbatim: no fixes, cite `file:line`, re-read each cited file.
3. Count severities, mark findings where two specialists converge.
4. Run the verification pass, mandatory: a separate agent that only confirms, downgrades, or rejects.
5. Report pass rate, convergence, blockers each with a one-line "why it ships broken", grouped highs, a pattern summary, one next action.

## What this skill will not do

- No style nits while a correctness finding is open.
- No rewriting the author's code unasked. A finding names the fix, the author writes it.
- No "looks fine" verdict without pasted test output.
- No finding without `file:line` and a reproduction, unless labelled `SUSPECTED`, and no invented findings on clean code.

## What bad output looks like

| Anti-pattern | Fix |
|---|---|
| Fifteen nits, no severity, no reproduction | Rank by severity, drop nits while a Blocker is open. |
| Every concatenation flagged, source untraced | Trace the value to attacker-controlled input, or file it `SUSPECTED`. |
| Checklist of headings, no edge case named | Name the empty input, boundary value, expired token, double submit. |
| Audit that reads only the README | Cite `file:line` in a file you opened, one agent verifies another. |

## Verification

- All modes: inputs printed, standards.md read, baseline 1 to 7 with output.
- FIND-BUGS, SECURITY: audit printed, every finding carries `file:line` plus a reproduction or the `SUSPECTED` label. SECURITY adds an OWASP code per finding and the ASVS bar.
- QA-CHECKLIST: `grep -c "^- \[ \]" <file>` greater than zero. WEBAPP-TEST: run output and console errors pasted, browser closed.
- PRE-LAUNCH: verification ran, pass rate stated, no specialist is last word on its own claim.
- Before returning: `grep -nP "\x{2014}|\x{2192}" SKILL.md references/*.md` is empty.

## Changelog
- [2026-07-03] Suite created from find-bugs, security-review, qa-checklist, webapp-testing, pre-launch-audit.
- [2026-08-28] Rebuilt: standards.md sourcing, a baseline run by command, one finding format, OWASP codes and the ASVS bar, an inputs block for context-free subagents, a refusal list, an anti-pattern table. Local tripwires moved to `references/local-context.md`. Mode names unchanged.
