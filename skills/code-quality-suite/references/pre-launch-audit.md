# Pre-Launch Audit Playbook

The full protocol behind PRE-LAUNCH mode. Read this before running a whole-repository audit.

## Purpose

Audit a codebase before it goes public. Six specialist passes analyse in parallel, then an
independent verifier re-reads every cited file and confirms, downgrades, or rejects each claim.
Output: a severity-ranked fix list (Blocker, High, Medium, Low) where every finding carries a
`file:line` citation that the verifier read for itself.

**Key principle:** no agent gets the last word on its own claim. Convergent findings, the ones two
or more specialists flag independently, are the highest-signal output of the run.

## When to use

- Before a repository goes public.
- Before a major release.
- After a large refactor, to confirm nothing regressed.
- When someone wants a second opinion on a repository that is about to ship.

## When not to use

- A single-file change. Use FIND-BUGS mode.
- Active development. This is a ship-readiness gate, not a work-in-progress check.
- When only one specialist view is wanted. Run that one pass directly.

## Protocol

### Step 0: state the plan and the scope

State in two or three sentences what will run, roughly how long it takes, and that the deliverable
is a report. Unless fixes were explicitly authorised, this is analysis only. Nothing is pushed.

### Step 1: get the repository on disk

The specialists need real files to read.

```bash
mkdir -p /tmp/audit && cd /tmp/audit && rm -rf <repo-name>
gh repo clone <owner>/<repo>
```

If `gh auth status` fails, ask the caller to authenticate or to give a path to an existing clone.

### Step 2: recon before dispatch

Build the brief that every specialist prompt carries as preamble:

- Directory tree to depth 2: `find . -type d -not -path '*/node_modules*' -not -path '*/.git*'`
- `package.json`: stack, dependencies, scripts
- Config files: build config, deployment config, framework config
- Route or entry-point inventory
- Migration files
- Total lines of code
- Existence checks: `.env.example`, CI workflow directory, test directory, error and loading boundaries

Every specialist prompt needs this stack context. An agent that has to rediscover the stack spends
its budget on recon instead of findings.

### Step 3: dispatch six specialists in parallel

Send one message containing all six agent calls so they run concurrently. Running them in sequence
costs five times the wall-clock time for the same result.

| Specialist | Scope |
|---|---|
| Security and auth | authn and authz, row-level policies in application code, secrets, XSS, CSRF, prompt injection, rate limits, scheduled-job auth |
| Performance | rendering strategy, fetch patterns, caching, bundle size, fonts, Core Web Vitals |
| Database | access policies, schema, indexes, migrations, query patterns, race conditions |
| Architecture | structure, error handling, type rigour, duplication, edge cases, dead code, test coverage |
| UX, accessibility, SEO | loading and error states, accessibility, mobile, forms, metadata, robots and sitemap |
| DevOps and dependencies | CI, environment variables, monitoring, regions, scheduled-job operations, dependency hygiene |

Use a specialist agent type where one matches the scope, otherwise `general-purpose`. When
`references/local-context.md` exists it names the agent types available in this environment.

Every specialist prompt must include:

1. The repository path and the stack context from recon.
2. Its single scope from the table above, expanded into sub-bullets.
3. This output format:

```
## [Specialist] Report
### Findings (Blocker, then High, then Medium, then Low)
- [SEV] Title
- File:line: path:42
- Claim: precise description
- Why it matters at scale: the real consequence
- Evidence: a code quote under 15 words
- Confidence: High, Medium, or Low
- Self-verified: re-read the file before submitting, yes or no
### Self-check notes
- Assumptions verified
- Mistakes caught before submitting
- What I could not verify
```

4. These hard rules, repeated verbatim in the prompt:
   - No fixes. Analysis only.
   - Every claim cites `file:line`.
   - Re-read each cited file before submitting.
   - Cap around 1,500 words. Quality over quantity.
   - Focus on what bites at production scale, not style.

### Step 4: collect the reports

As each specialist returns, relay one line, its headline finding. Do not relay full reports. When
all six are back, count claims by severity and identify convergent findings, anything flagged by
two or more specialists independently.

### Step 5: independent verification pass

Compile the full claim list with numbered IDs by category prefix (S1 to S12, P1 to P13, and so on)
and dispatch one verifier agent. Its prompt must carry:

1. The repository path.
2. The complete numbered claim list with `file:line` citations.
3. Its protocol: read each cited file, or confirm the claim that a file is missing. Mark each claim
   CONFIRMED, REJECTED, or PARTIAL with an adjusted severity. Note which specialists converged on a
   shared finding. Add no new findings, verify only what was submitted. Output convergent findings,
   then verified findings by severity, then rejected and downgraded, then inconclusive, then an
   independent ranking of the top 10 launch blockers.

Cap the verifier output at around 3,000 words.

### Step 6: the final report

1. Header line: "X of Y claims verified. Z severity-adjusted. N rejected." A rejection rate above
   15 percent means the specialist prompts are too loose, not that the verifier is too strict.
2. Convergence note: the findings multiple specialists reached independently.
3. Launch blockers table: file, issue, why it ships broken.
4. Highs, grouped by area.
5. Mediums, summarised at the pattern level rather than listed exhaustively.
6. Lows, one block of bullets.
7. Severity adjustments table: original, adjusted, reason.
8. Where the run was logged, when a log path applies.

### Step 7: capture the learnings

Append reusable, cross-project patterns to the past-mistakes and decisions files named in
`references/local-context.md` when that file exists. Without it, put the same content in a section
at the end of the report. Log a note even when the audit finds little, a clean baseline is useful
evidence later.

### Step 8: recommend the next move

End with one specific action, not an open question. For example: "Fix in this order: B1, B2, B6,
B8. That closes the largest blast-radius gaps in under a day." Or offer to draft the issues, or to
re-run after the fixes merge.

## Hard rules

- Never push fixes. This is a read-only audit.
- Never let an agent be the last word on its own claim. The verification pass is mandatory.
- Always cite `file:line`. "The code is messy" is not a finding.
- Convergent findings lead the report.

## Anti-patterns

- One mega-agent asked to "audit everything". Shallow in every domain.
- Skipping verification. Over-claims survive into the report and cost the reader trust.
- Listing every nit. Cap at the top 10 blockers plus a clean Medium and Low summary.
- Auditing without cloning. The agents have no files to read and answer from the README.
- Running the specialists sequentially.

## Output quality bar

- Each of the top 10 blockers has a one-line "why it ships broken". The table alone should convey
  the launch risk.
- Convergence is called out explicitly.
- Severity adjustments are listed transparently, which is the evidence that the system self-corrects.
- Learnings are captured before the report is presented, not promised for later.
- The report ends with one recommended action.

## Changelog
- [2026-04-18] Playbook created from a six-specialist audit run: 100 claims dispatched, 86 verified as stated, 5 downgraded, 0 rejected.
- [2026-08-28] Genericised for publication. Persona names, owner name, agent-type names, and vault paths moved to `references/local-context.md`.
