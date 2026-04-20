# pg-startup-eval — The Definitive Startup Idea Evaluator for Claude

Stop getting vague AI feedback on your idea. This skill applies 17 investor and founder frameworks, runs live market research, and ends with a forced verdict — Strong, Weak, or Pivot Required — with specific reasons.

## What It Does

Most AI feedback on startup ideas is encouraging mush. This skill evaluates any startup, product idea, or side project the way a rigorous investor would: by stress-testing assumptions, surfacing structural risks, and finding the fatal flaws before money and time are wasted.

It applies 17 frameworks across 10 evaluation phases — from problem severity and market sizing to moat analysis and unit economics — and ends with one non-hedged verdict plus a roadmap of next steps. It also auto-detects business type (software vs. physical/capital vs. service) and shifts the evaluation lens accordingly.

## Frameworks Applied (17+)

| Framework | What It Evaluates |
|---|---|
| Paul Graham (YC) | Organic vs. sitcom origin, fatal mistake checklist, schlep/unsexy filter, default alive test |
| Peter Thiel (Zero to One) | 7 Questions, the Thiel Secret, 10x test, monopoly structure |
| Marc Andreessen (PMF) | Product-market fit signal, distribution as strategy |
| Sequoia Capital | 10-block scorecard across purpose, problem, solution, team, market |
| Bill Gurley | Bottom-up market sizing methodology, "market you can win" framing |
| Steve Blank | Customer development stages, problem vs. solution interviews |
| Rob Fitzpatrick (Mom Test) | Commitment ladder (Level 0–3), validation conversation structure |
| Clayton Christensen (JTBD) | Functional, emotional, and social job layers |
| Hamilton Helmer (7 Powers) | Scale economies, network effects, switching costs, counter-positioning, cornered resource, process power, branding |
| Geoffrey Moore (Crossing the Chasm) | Beachhead market sizing and dominance test |
| Eric Ries (Lean Startup) | Fake door test, concierge test, vanity vs. real metrics |
| Alexander Osterwalder | Value Proposition Canvas — fit between jobs, pains, and gains |
| Jeff Bezos | Working Backwards press release test, hardest FAQ method |
| Ben Horowitz | Business model alignment — pricing must match value delivery |
| First Round Capital | Domain access, learning velocity, obsessive problem proximity |
| a16z | Counter-positioning lens: structural vs. executional reasons incumbents can't copy you |
| Bill Gross (Idealab) | Timing as the #1 factor — enabling wave identification |

## What You Get

Every evaluation produces a 14-section output:

1. **Market Research Findings** — competitive landscape, incumbents, pricing, recent investment activity
2. **Idea Classification** — business type, origin (organic vs. sitcom), current validation level
3. **The Thiel Secret** — what the founder knows that most people don't; flagged as absent if not articulable
4. **Jobs-to-Be-Done Analysis** — functional, emotional, and social job layers mapped
5. **Why Now — Enabling Wave** — the specific technology, behavior, or regulatory change that makes this the right moment
6. **Market Size — Bottom-Up** — customer count × realistic conversion × ACV; Year 1 and Year 3 projections
7. **Thiel's 7 Questions** — rated Strong / Weak / Unknown across engineering, timing, monopoly, people, distribution, durability, and secret
8. **The 10x Test** — the one dimension of superiority; a working-backwards press release in customer language
9. **Business Model** — CAC, LTV, LTV/CAC ratio, payback period, gross margin, default-alive assessment
10. **Go-to-Market** — distribution model, first 100 customers, growth loop, beachhead dominance timeline
11. **Defensibility — 7 Powers Assessment** — each power rated active now / buildable in 12 months / buildable in 3 years / not applicable; 18-month clone test
12. **Founder and Team Fit** — domain insight, access to early customers, bias toward action, PG fatal mistakes
13. **Validation Status** — current commitment level (0–3), path to Level 3 validation in 30 days
14. **Sequoia Scorecard** — 10-block rating; Three Fatal Flaws; Final Verdict

## Evaluation Proof — 5 Real Ideas Tested

| Idea | Type | Verdict | Key Insight Surfaced |
|---|---|---|---|
| Dog walking app | B2C Marketplace | PIVOT REQUIRED | Rover already has vet chat; market is solved infrastructure; no enabling wave justifies a new entrant |
| AI contract review for law firms | B2B SaaS | WEAK | No tech co-founder for a hard ML problem; "the model learns the firm's playbook" claim is unproven; 18-month window is closing as BigLaw deploys Harvey |
| Async video standup tool | B2B SaaS | WEAK | Atlassian owns Loom + Jira + Rewatch and can bundle this feature free within 18 months; no counter-positioning against the bundle |
| PMDojo (PM learning app) | B2C Consumer | WEAK | Quiz gate is a 2-sprint add for any PM newsletter; B2C ceiling without a B2B motion; beachhead of "aspiring PMs" is too broad to dominate |
| EV charging franchise (India) | Physical Infrastructure | WEAK | Franchisor ROE projections assume 50% charger utilization; documented real-world average in India is 5–25%; operator bears all capital risk while the platform captures brand value and data |

## How to Install

### Claude Code (Recommended)

1. Clone this repository into your Claude skills directory:

```bash
git clone https://github.com/Anmoll-W/pg-startup-eval ~/.claude/skills/pg-startup-eval
```

That's it. Claude Code auto-discovers skills in `~/.claude/skills/` — no settings file changes needed.

2. Use it in any Claude Code session:

```
/pg-startup-eval
```

Or just describe your idea naturally — the skill is triggered by evaluation-intent phrases like "what do you think about this idea?", "is this worth pursuing?", or "I was thinking of building X."

### Manual Use (Without Claude Code)

Copy the contents of `SKILL.md` into any Claude conversation as a system prompt, then describe your idea.

### What Gets Asked

Before evaluating, the skill asks for exactly five things:

1. The idea — in plain language, one paragraph
2. Target customer — who specifically has this problem
3. Idea origin — did this come from lived experience with the problem, or was it brainstormed as a business opportunity?
4. Current user conversations — have you spoken to anyone with this problem? What did you hear?
5. Idea type — B2B SaaS / B2C / Marketplace / Consumer app / Hardware / Service / Other

The evaluation does not proceed until all five are answered. This is intentional — the input quality determines the output quality.

## Example Output Structure

Each section is 3–8 sentences, specific to the idea, with no generic startup advice. The Three Fatal Flaws section explicitly rules out phrases like "execution is hard" or "competition exists" — every flaw must be specific to the idea being evaluated.

The Final Verdict section is one of three options with no hedging:

- **Strong** — enabling wave exists, problem is severe and frequent, 10x differentiation is believable, unit economics work, distribution is identified, founder has asymmetric insight, at least 2 of Helmer's 7 Powers are buildable
- **Weak** — 1–3 of the above fail; states exactly what must change and which hypothesis must be validated first
- **Pivot Required** — the idea as stated won't work; proposes one specific adjacent idea worth exploring based on the founder's domain and the customer pain that was identified

## Skill Chaining

After a verdict, the skill recommends the appropriate next action:

**If Strong:**
- `/spec-miner` — mine requirements from customer conversations
- `/feature-forge` — design the MVP feature set
- `/marketing-skills:launch-strategy` — build the GTM plan
- `/marketing-skills:customer-research` — run formal discovery

**If Weak:**
- Return to this skill after validating the single most important hypothesis

**If Pivot Required:**
- `/superpowers:brainstorm` — generate adjacent idea variants

**For all verdicts:**
- `/investment-agent` — simulated investor conversation
- `/grill-me` — stress-test the pitch
- `/architecture-designer` — design the technical system when it's time to build

## Reference Files

The skill includes four reference documents used during evaluation:

- `references/market-sizing.md` — Gurley's bottom-up methodology in full detail
- `references/moat-frameworks.md` — Complete 7 Powers breakdown with real examples and early-stage tests
- `references/validation-playbook.md` — Mom Test + Blank + Ries validation methods with specific conversation templates
- `references/output-template.md` — Exact output format for each of the 14 sections

## Contributing

**Submit an idea for evaluation:** Open an issue with your idea, target customer, and idea origin. Ideas evaluated publicly will be added to the proof table above with your permission.

**Improve a framework:** If a framework application is wrong, shallow, or outdated, open a PR with the specific section in `SKILL.md` and the proposed change. Include the source (paper, book, talk) for any factual claim.

**Add a framework:** New frameworks must earn their place — they must catch failure modes not already covered by existing frameworks. Open an issue first to discuss before writing a PR.

## License

MIT — use, fork, and adapt freely. Attribution appreciated but not required.
