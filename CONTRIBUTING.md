# Contributing

Thank you for looking. These skills exist because a real PM workflow kept
breaking in the same place, and someone sat down to fix it. Contributions that
carry that spirit are welcome.

## The bar every skill here has to clear

A skill in this repository is not a prompt. It is a contract with a verification
section that a machine can run. Before a change lands, it has to pass the same
gate the skill already passes.

1. **A mode is named before it runs.** No skill guesses what you meant and then
   silently does something else.
2. **Every claim carries a source.** A finding cites a file and a line, or a
   rule, or a command that produced the number. A claim with no source gets a
   label that ranks it last, never a blocker.
3. **The skill degrades honestly.** When a local context file is absent, the
   skill still runs and says what it skipped. It never invents a path, a name,
   or a count to look complete.
4. **The verification section is mechanical.** It is a list of commands, not a
   list of hopes. If you add behaviour, add the check that proves it.

## How to propose a change

1. Open an issue first. Describe the workflow that broke and the moment it broke
   in. A good issue reads like a bug report from a real session.
2. Keep the diff small. Fix the root cause at the shared point, not the symptom
   at one caller.
3. Run the skill's own verification section and paste the output in the pull
   request. A change with no pasted output is not ready.
4. No em dashes and no arrow characters anywhere the skill writes. This is
   enforced by a grep in most verification sections. Use a period, a comma, or a
   colon.

## What this repository will not accept

- A new mode with no verification gate.
- A metric with no run behind it.
- Third-party material with the credit stripped off. If you bundle a reference,
  the license travels with it and the NOTICE names it.

## License

By contributing, you agree that your contribution is licensed under the MIT
License that covers the original work in this repository. Third-party bundled
material keeps its own license, recorded in NOTICE.md.

Built and maintained by [The PM Code](https://www.linkedin.com/company/the-pm-code/).
