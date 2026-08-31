# Code Review Standards

Published standards paired with this owner's tripwires.

## 1. Review scope and size

Look for design, functionality, complexity, tests, naming, comments, style, consistency, documentation (Google, 2026-08-28, https://google.github.io/eng-practices/review/reviewer/looking-for.html). Keep changes near 100 lines, not past 1000, same source: https://google.github.io/eng-practices/review/developer/small-cls.html. Detection falls past 200 to 400 lines, or 500 per hour (SmartBear/Cisco study, 2026-08-28, https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/).

## 2. Security review baseline

| Code | OWASP Top 10:2021 category |
|---|---|
| A01 | Broken Access Control |
| A02 | Cryptographic Failures |
| A03 | Injection |
| A04 | Insecure Design |
| A05 | Security Misconfiguration |
| A06 | Vulnerable and Outdated Components |
| A07 | Identification and Authentication Failures |
| A08 | Software and Data Integrity Failures |
| A09 | Security Logging and Monitoring Failures |
| A10 | Server-Side Request Forgery (SSRF) |

Source, 2026-08-28: https://owasp.org/Top10/2021/A00_2021_Introduction/; 2025 edition live: https://owasp.org/Top10/2025/. Default bar: ASVS Level 1, easily discovered flaws in the Top 10, pen-testable, same date: https://github.com/OWASP/ASVS/blob/master/4.0/en/0x03-Using-ASVS.md.

## 3. Test expectations

A bug fix ships a failing-then-passing test; no bug counts as fixed without one (Martin Fowler, 2026-08-28, https://martinfowler.com/articles/testing-culture.html). New logic names edge cases: empty input, boundary values, error paths.

## 4. Owner tripwires

Environment-specific rules live in `references/local-context.md`, which this skill reads
if present. That file holds the tripwire list and the command that checks each one. If
it is absent, run items 1 to 5 of the checklist below, skip items 6 to 12, and say in the
report that no local tripwire file was found.

## 5. Review checklist (per command)

Items 1 to 5 are universal. Items 6 to 12 come from `references/local-context.md` and apply
only when that file exists.

1. Tests run, output pasted.
2. Diff size: `git diff --stat`, split past ~400 lines.
3. Secrets: `grep -rniE "(api[_-]?key|secret|password|token)\s*=\s*['\"]" <files>` clean.
4. Markers: `grep -rn "TODO\|FIXME" <files>` none unlinked.
5. Migrations: `git diff --name-only main -- '*migrations*'` only new.
6. Cron exports: `grep -n "export async function GET\|export async function POST" <route>` both present.
7. Cron auth: `grep -n "CRON_SECRET" <route>` present.
8. Numeric reads: `grep -n "parseFloat(String(" <file>` present.
9. RLS: queries run as non-admin, not just service-role.
10. External content fenced: `grep -n "<external_content>" <file>` wraps scraped or RSS/Reddit/HN text.
11. Counters: SQL uses `set x = x + 1`, not JS read-then-write.
12. Reward or access catch blocks: return failure shape, not silent success.

## 6. Refresh by 2026-11-28

Recheck:
- https://google.github.io/eng-practices/review/reviewer/looking-for.html
- https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/
- https://owasp.org/Top10/2025/
- https://github.com/OWASP/ASVS/blob/master/4.0/en/0x03-Using-ASVS.md
