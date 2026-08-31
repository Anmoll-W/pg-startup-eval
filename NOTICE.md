# Notice

Most of the work in this repository is original. Five skills are written from
scratch: decoder, decision-support, teach, prompt-generator, and pg-startup-eval.
Two skills bundle third-party reference material alongside original mode logic,
and that material keeps its own license. This file records it plainly.

The rule is simple. The mode logic, the finding formats, the verification gates,
and the way the skills fit together are original PM Code work under MIT. Where a
skill folds in an outside reference, the outside reference stays under its own
terms, and the credit sits next to the code that uses it.

## code-quality-suite

Two of its five modes read from bundled references that are not original.

- **SECURITY mode** reads `references/security-review/`, derived from the OWASP
  Cheat Sheet Series, licensed Creative Commons Attribution-ShareAlike 4.0
  International (CC BY-SA 4.0). Source: https://cheatsheetseries.owasp.org/ .
  The full license text is retained at
  `skills/code-quality-suite/references/security-review/LICENSE`.

- **WEBAPP-TEST mode** reads `references/webapp-testing/`, a Playwright driver
  reference licensed under the Apache License 2.0. The full license text is
  retained at `skills/code-quality-suite/references/webapp-testing/LICENSE.txt`.

Full detail: `skills/code-quality-suite/NOTICE.md`.

## design-review-suite

Its DESIGN-SYSTEM and AUDIT modes read from two bundled references that are not
original.

- **ui-ux-pro-max**, a searchable UI and UX pattern database, MIT licensed,
  Copyright (c) 2024 Next Level Builder.
  Source: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill .

- **web-design-guidelines**, folded into AUDIT as an optional rule source, MIT
  licensed, Copyright (c) 2025 Vercel Labs.
  Source: https://github.com/vercel-labs/web-interface-guidelines .

Full detail: `skills/design-review-suite/NOTICE.md`.

## Everything else

decoder, decision-support, teach, prompt-generator, and pg-startup-eval are
original, MIT licensed, Copyright (c) 2026 Anmoll Wadhwa (The PM Code).
