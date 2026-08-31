# QA Checklist Playbook

The full protocol behind QA-CHECKLIST mode. Generate a comprehensive, source-grounded test
checklist for a project, a feature, or a non-code artifact. Read this before writing a checklist.

## When to use

- Picking up a project for the first time, or after a long gap.
- Before a feature ships.
- Before a ship-readiness sign-off.
- When any agent wants its own output stress-tested before presenting it.

## Step 1: read before you write

Never generate a checklist from memory. Read the actual source first.

| Context | What to read |
|---|---|
| Code project | Every screen, component, API call, state management pattern, auth boundary |
| Spec or PRD | Every user story, acceptance criterion, edge case section |
| Content | Full text, every claim, every link, every call to action |
| Decision | Full context, every assumption, every dependency |
| Financial model | Every formula, every input assumption, every output |

## Step 2: generate the checklist

Group by feature or screen. Every item in this format:

```
- [ ] Test description, expected result
```

Cover all eight categories for every feature or screen.

**1. User flows (happy paths).** Every golden path a real user takes, entry to success state.

**2. Edge cases and error states.** Empty inputs, null values, max-length strings. Invalid formats
(email, phone, URL). Duplicate submissions and double clicks. Concurrent users and race conditions.
Expired tokens or stale data. Zero state (no items, no results, no data yet).

**3. Auth and session handling.** Login, logout, token expiry. Unauthenticated access to protected
routes. Role-based access (admin, user, guest). Session persistence across refresh and tab close.
OAuth edge cases (cancelled flow, denied permissions).

**4. API failures and loading states.** 400, 401, 403, 404, 500. Slow network and timeout behaviour.
Partial loads where some data arrives and some fails. Skeleton and loading states, do they appear
and resolve. Retry logic, does it retry and does it stop.

**5. Navigation and deep links.** Back button, browser and in-app. Direct URL access to every route.
Refresh on each screen. Missing or malformed route params. Redirect logic after login and logout.

**6. Offline and no internet.** What breaks completely, what degrades gracefully, what shows a clear
error rather than failing silently, and whether the app recovers when the connection returns.

**7. Performance checkpoints.** First meaningful paint. List rendering with 100 or more items. Rapid
repeated actions. Asset load on a slow connection. Memory growth over a long session.

**8. Platform and accessibility.** Mobile at 375px and 768px, desktop at 1440px. Keyboard navigation
(tab order, Enter to submit, Escape to close). Touch targets at 44px minimum. Screen reader labels
(`aria-label`, `role`). Colour contrast at WCAG AA, 4.5:1 for body text.

A category heading with no case named under it is not coverage.

## Step 3: save the checklist

Save to the checklist path in `references/local-context.md` when that file exists, otherwise to
`docs/qa-checklist.md` in the repository under test. Header:

```markdown
---
project: [name]
generated: YYYY-MM-DD
last-updated: YYYY-MM-DD
---

# QA Checklist: [Project Name]
```

## Step 4: after testing

- `- [x]` passed.
- `- [!]` failed. Add `FAIL: [what happened] | Expected: [expected] | Repro: [steps] | Severity: blocker/major/minor`.
- `- [-]` not applicable, with the reason.

Route failures to the owner of the domain they belong to. `references/local-context.md` names those
owners when it exists; without it, report them all to the caller.

## Cross-domain use

The method is not only for code.

| Artifact | What the checklist covers |
|---|---|
| Content | Every link, every call to action, mobile render, formatting, factual accuracy |
| Research or financial model | Are the conclusions falsifiable, which inputs break the model, which assumptions have untested edges |
| Spec | Which scenarios are unspecified, which user stories have unnamed edge cases |
| Design | Accessibility, touch targets, responsive behaviour, colour contrast |

## Changelog
- [2026-04-16] Playbook created.
- [2026-08-28] Genericised for publication. Owner names, persona routing, and vault save paths moved to `references/local-context.md`.
