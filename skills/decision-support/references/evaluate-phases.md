# EVALUATE phases, the full ten

The contract, the output shape and the hard stops live in `SKILL.md`. This file holds the
questions each phase asks. Read it before running EVALUATE. If it is absent, `SKILL.md`
alone is still runnable: grade the ten scorecard blocks directly and say that the phase
detail was unavailable.

Frameworks drawn on, named so the buyer can check the source: Paul Graham, Peter Thiel
(Zero to One), Marc Andreessen, Sequoia Capital, Bill Gurley, Steve Blank, Rob Fitzpatrick
(The Mom Test), Clayton Christensen (Jobs to Be Done), Hamilton Helmer (7 Powers),
Geoffrey Moore (Crossing the Chasm), Eric Ries (Lean Startup), Jeff Bezos (Working
Backwards), Ben Horowitz.

## Phase 0, gather input and calibrate

Ask for all five before proceeding. Do not proceed until all five are answered.

1. The idea in plain language, one paragraph at most.
2. Target customer, who specifically has this problem.
3. Idea origin, lived experience with the problem or brainstormed as an opportunity.
4. Conversations held so far, and what was actually heard.
5. Idea type: B2B SaaS, B2C, marketplace, consumer app, hardware, service business, other.

Then switch the evaluation to match the type.

**Software (B2B SaaS, B2C, marketplace, consumer app).** Run the phases as written. Unit
economics in LTV, CAC and ARR terms.

**Physical or capital deployment (infrastructure, franchise, hardware, real estate,
manufacturing).**
- Replace ARR targets with IRR and payback period on equity deployed.
- Replace LTV over CAC with revenue per unit, times utilization, times margin, against
  capex per unit.
- The market question becomes the realistic return on capital at realistic utilization,
  not TAM.
- The moat question becomes what stops the host site, franchisor or supplier from
  restructuring terms against the operator as they scale.
- Run three utilization scenarios: stress at 10 percent, base at 25, bull at 50. The
  stress case must be survivable.
- Treat any ROI projection supplied by a franchisor or platform partner as marketing math
  until it is checked against independent utilization data.
- Most commonly missed flaw: the operator carries the risk while the platform captures the
  brand and the data.

**Service, consulting or agency.**
- Replace ARR with annual billings and utilization rate.
- The moat question becomes whether this is a people business or a process business.
  People businesses do not scale, process businesses can.
- Most commonly missed flaw: revenue is linear with headcount unless a productized service
  or an IP layer is built.

## Phase 1, live research before any opinion

Run the research first. A founder's market assumptions are the most commonly wrong input
in any evaluation, so nothing is graded until the landscape has been looked at.

- The competitive landscape: the top three to five incumbents, what they charge, how they
  are positioned.
- The why now signal: technology, regulatory or behavioural shifts in the last two to
  three years.
- Investor activity in the space, as a read on timing and on incoming competition.
- A bottom up estimate of the real addressable market. Method in `market-sizing.md`.

Surface what was found with its source. Never present a recalled figure as a researched one.

## Phase 2, problem reality and jobs to be done

**The three job layers (Christensen).** Functional, what they are trying to accomplish.
Emotional, how they want to feel. Social, how they want to be seen. Map the idea against
all three. A product serving only the functional layer is easy to switch away from.

**Problem severity.** What is the customer doing right now instead, because the workaround
is the real competitor. What does the problem cost per week or month. Is this hair on fire
or back burner. Blank's test: does it rank in the customer's top three priorities this
quarter. If not, they will not pay to fix it.

**Organic or sitcom (Graham).** Organic ideas come out of lived experience and carry
asymmetric insight. Sitcom ideas are worked backwards from what would make a good startup,
and have a structurally lower hit rate. Say which this is and what it implies.

## Phase 3, market

**Why now, the enabling wave.** Name the specific change of the last two to three years
that makes this the moment: a technology wave that made the solution far cheaper, a
behaviour wave where users adopted a prerequisite habit, or a regulatory wave that opened a
market. If nothing structural changed, flag it. An idea with no tailwind fights gravity.

**Bottom up sizing (Gurley).** Top down TAM is a fiction exercise. Define the specific
customer unit, count it, estimate what the chosen channel can reach in year one, model
revenue per customer, then work forward and check top down only as a sanity test. Full
method in `market-sizing.md`.

**The Thiel secret test.** What does the founder know about this market that a smart person
reading the same industry reports would not know. Generic answers, that the market is
growing or that customers are frustrated, are not secrets.

## Phase 4, solution and differentiation

**The 10x test.** Name the one dimension where this is or could be ten times better, not
ten percent better on five dimensions. Confirm that dimension is the one the customer ranks
first, and say whether 10x is reachable now or only at scale.

**Thiel's seven questions.** Engineering, timing, monopoly, people, distribution,
durability, secret. Answer all seven. If more than two cannot be answered confidently, name
which and what is missing.

**Working backwards (Bezos).** Write the press release in customer language, then the three
hardest FAQs. If the release is vague or could describe five different products, the value
proposition has not been found yet.

## Phase 5, business model and unit economics

Model one customer from first contact to contract end before discussing scale: fully loaded
CAC, realistic LTV, payback period, gross margin. Minimum viable ratios are LTV over CAC of
at least 3 to 1 and payback within 18 months. Best in class is 5 to 1 and payback within 6
months. If the model only works at scale, that requires a stated bridge strategy.

**Default alive or default dead (Graham).** At the current burn and growth rate, does the
company reach profitability before the money runs out with no further raise. An unanswerable
question here is itself a red flag.

**B2C specifics.** Consumer economics differ structurally from B2B SaaS.
- Retention cliff: consumer habit and learning apps commonly run 5 to 8 percent monthly
  churn against 1 to 2 percent in B2B SaaS. Model two churn scenarios explicitly.
- Two viable modes: very large scale with a real freemium engine, or a small profitable
  lifestyle business. The middle is where consumer learning tools die. Say which mode this
  is, and if it is the middle, say why it escapes.
- Re-engagement mechanic: what brings a user back after a broken streak or a missed week.
  Designed in, never assumed.
- Viral loop: without one, CAC scales linearly forever and the maths works only while the
  warm network lasts.
- Expansion path: if venture scale requires teams or employers paying, that architecture
  belongs in year one, not retrofitted.

**Pricing alignment (Horowitz).** Is the pricing model aligned with where the value lands.
Charging per seat when value comes from usage produces under-licensing and churn.

## Phase 6, go to market and distribution

Distribution decisions made at launch are very hard to undo, and the product architecture,
pricing and onboarding all have to match the model chosen.

**Pick one of four models.** Product led growth, needing self serve value before payment.
Inside sales, working at 5,000 to 50,000 in annual contract value. Enterprise field sales,
above 50,000, with procurement, security review and a champion strategy. Channel or
partnership, which works only when the partner cannot serve the niche profitably itself.

**Growth loops, not funnels.** A funnel terminates, a loop compounds. Referral, data,
content and network loops are the four common shapes. Without at least one, CAC is
permanently linear.

**Beachhead (Moore).** Not a demographic, a nameable group small enough to dominate with
current resources inside 18 months.

**Do things that do not scale (Graham).** Has the founder personally closed the first ten
customers, done concierge delivery, recruited users by hand. This is both a validation
method and a founder quality signal.

## Phase 7, defensibility

Run Helmer's seven powers and say, for each that applies, when it activates and what has to
be built to get it. Fewer than two buildable powers means the business is structurally
vulnerable. Then run the 18 month clone test: a well funded team with the same insight
starts building, and the answer to why they lose has to be something that accumulates in
the business, never a head start. Detail and worked examples in `moat-frameworks.md`.

## Phase 8, founder and team fit

- Insight, per Graham's test in phase 3, restated against the founder rather than the market.
- Domain access: can the founder reach the first fifty customers with no marketing budget.
  Cold outbound on day zero is a weak fit signal.
- Learning velocity: has the founder already changed their model because of evidence.
- Problem proximity: emotionally compelled, not intellectually interested.
- Graham's fatal mistakes, checked explicitly: single founder, marginal niche, derivative
  idea, no specific user in mind, launching too late, not listening to users.
- The schlep filter: is this being avoided by other founders because it is genuinely hard,
  which is an advantage, or because it is actually bad.

## Phase 9, validation status

Rank current evidence on the commitment ladder, where verbal enthusiasm counts as nothing.
Level 0 is talk, surveys and waitlists. Level 1 is a follow up call or a warm introduction.
Level 2 is a structured pilot, detailed requirements, or use of a manual version. Level 3 is
pre-payment, a letter of intent, or a card on file before the product exists. At level 0 or
1 the evaluation is working with hypotheses, not evidence, and must say so. Full ladder and
the interview rules in `validation-playbook.md`.

**PMF signal (Andreessen).** If the product is live: are customers pulling it, or is it
being pushed at them.

**Before building.** At level 0 or 1, name the minimum validation actions: twenty customer
conversations, a fake door test, a concierge test, one level 3 commitment.

## Phase 10, next steps and handoffs

Pick the next actions from the verdict, and pass the named context with each handoff.

**Strong.** Get level 3 validation before writing code. Mine requirements from the
conversations already run, quoting the problem statement verbatim. Design the MVP against
the beachhead and the 10x dimension. Then GRILL mode on the pitch, passing the scorecard and
the three fatal flaws.

**Weak.** Name the single most important hypothesis, design the cheapest test that confirms
or kills it, then GRILL mode on that hypothesis, passing the flaw ranked first. Run INVERT
first instead if the idea is stated as a solution with no established problem. Return to
EVALUATE once the test has run.

**Pivot required.** Generate adjacent pivots from the domain insight and the customer pain,
then CHALLENGE mode on each before starting a fresh evaluation cycle.

**Any verdict.** GRILL mode on the narrative before any investor conversation, once
validation reaches level 2. Price only after unit economics are modelled. Build the
competitive positioning narrative only after differentiation is defined.
