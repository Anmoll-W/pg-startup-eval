# Moat and Defensibility Frameworks

## Hamilton Helmer's 7 Powers — Full Reference

Source: "7 Powers: The Foundations of Business Strategy" — widely used by a16z, Sequoia, and other top-tier VCs for evaluating startup durability.

### 1. Scale Economies
Unit costs decline as volume increases. The business gets more efficient as it grows — cost per customer, cost per transaction, or cost per unit drops at scale.

**When it applies**: Data infrastructure, content production, physical logistics, manufacturing.

**Early-stage signal**: Can you describe a specific unit cost that will drop by >50% when you reach 10x current scale? If yes, name it and the mechanism.

**Trap**: Many SaaS companies claim scale economies via cloud hosting costs — this is usually too small to matter strategically.

---

### 2. Network Effects
Each new user makes the product more valuable for existing users. The product improves *automatically* as the network grows, with no additional work from the company.

**Most overused claim in startup evaluations.** Most products that claim network effects have engagement loops, not network effects.

**Test for genuine network effects**: Remove half the users. Does the value of the product for the remaining users meaningfully decrease? If not, there is no network effect.

**Types**:
- **Direct (same-side)**: Users connect to other users of the same type. Social networks, messaging apps, collaboration tools.
- **Indirect (cross-side)**: Two distinct user groups benefit from each other's participation. Marketplaces, platforms. The flywheel is: more buyers → more sellers → better prices/selection → more buyers.
- **Data network effects**: More users generate more data → better ML model → better product → more users. This is *not* automatic — it requires the feedback loop to actually improve the product for users. Many companies claim this but the loop is too slow or too noisy to matter.

**Local vs. global**: A network effect can be local (within a city, industry, or team) but not global (adding users in Tokyo doesn't help users in Toronto). Local network effects are real but less defensible than global ones.

---

### 3. Switching Costs
The cost of leaving — financial, operational, psychological, or time-based — creates stickiness. Customers stay not just because the product is great but because leaving is painful.

**Types**:
- **Data lock-in**: Customer data lives in your system in a proprietary format. Exporting is difficult or lossy.
- **Workflow integration**: The product is embedded in how work gets done. Switching requires retraining people and rebuilding processes.
- **Contract lock-in**: Multi-year contracts with termination penalties.
- **Learning curve**: Users have invested time learning the product; switching means starting over.
- **Ecosystem lock-in**: The product connects to other products in a suite; switching requires replacing the whole ecosystem.

**Consumer apps almost never have meaningful switching costs.** B2B products with deep workflow integration have very high switching costs.

**Early-stage signal**: Ask: "If a competitor launched the exact same product for free, how many customers would leave in 30 days?" If the answer is "most," switching costs are near zero.

---

### 4. Counter-Positioning
Your business model is structurally incompatible with the incumbent's P&L, so they can't copy you without destroying their core business. This is the most underrated and underused moat at early stage.

**The canonical example**: Netflix vs. Blockbuster. Netflix's unlimited streaming subscription required eliminating late fees — but late fees were ~70% of Blockbuster's store revenue. Blockbuster couldn't replicate Netflix's model without committing financial suicide.

**The formula**: The incumbent has a high-margin line of business that your model would cannibalize. They rationally choose not to compete because the cure is worse than the disease.

**How to identify it**: Ask "What would it cost the market leader to build exactly what we're building?" If the answer is "it would destroy their existing revenue/margins/relationships," you have counter-positioning.

**Early-stage application**: Is there a structural reason the incumbent can't or won't copy you? Not because they're slow or lazy — but because doing so would harm their core business?

---

### 5. Branding
Durable brand creates pricing power and customer preference that persists even when cheaper or technically superior alternatives exist.

**Not applicable at early stage.** Takes 7-10 years of consistent positioning to build. Don't evaluate early-stage ideas on branding potential.

**Exception**: If the founder brings an existing personal brand that gives them privileged access to the target customer — this is a cornered resource (Power #6), not branding.

---

### 6. Cornered Resource
Exclusive or preferential access to a unique asset that competitors cannot easily replicate. The asset can be: proprietary data, regulatory approval, exclusive distribution contract, key talent, physical resource, IP.

**Examples**:
- A healthcare startup with exclusive data partnerships with 50 hospital systems
- A fintech with regulatory licenses that take 18-24 months to obtain
- A marketplace that has signed exclusive supply agreements with the top 20% of providers in a category
- A founder who is personally the most credible operator in the space (talent-as-resource)

**Early-stage test**: "What do we have access to that a well-funded new entrant could not obtain in the next 18 months?"

---

### 7. Process Power
Operational complexity embedded in the organization — accumulated over time — that cannot be replicated simply by hiring the same people or buying the same tools.

**Examples**: Toyota's production system (TPS). Amazon's fulfillment operations. SpaceX's manufacturing processes.

**Not applicable at most early-stage evaluations** — process power is built, not designed. It accumulates through years of iteration, failure, and refinement. You can't have it on day one.

**Exception**: A founder who spent 10 years building operational expertise in a domain can bring process power as a founding asset — but this must be specific and demonstrable, not just "we have operational expertise."

---

## The 18-Month Clone Test

A well-funded team (say, $10M, ex-Google engineers, domain experts) learns your thesis today and starts building. Why do they lose?

**Unacceptable answers**:
- "We have a head start" — time is not a moat
- "We move faster" — speed is temporary
- "We know the customer better" — knowledge can be acquired
- "Our team is better" — talent can be hired

**Acceptable answers** (cite which Power is activating):
- "By then, we'll have 200K users and a data flywheel producing training data they can't replicate" (data network effect)
- "Our customers will have built workflows around us; switching requires 3 months of retraining" (switching costs)
- "The incumbent can't copy our pricing model without cannibalizing their existing contracts" (counter-positioning)
- "We'll hold exclusive data agreements with the top 10 hospitals in the category" (cornered resource)

---

## Thiel's Monopoly Framework

A business worth building aims to monopolize a specific small market, then expand. The moat is not about defending against all competitors — it's about achieving a position where competing in your specific niche becomes economically irrational for others.

**The sequence**:
1. Dominate a small, specific beachhead with such force that competition there becomes irrelevant
2. Expand into adjacent markets from a position of strength
3. Repeat

**Thiel's monopoly ingredients** — a business has monopoly characteristics when it has at least 2 of:
- Proprietary technology (10x better than next best)
- Network effects (product improves as network grows)
- Economies of scale (business model gets better as it grows)
- Branding (durable customer perception commanding a premium)

At early stage: which two are you building toward, and when do they activate?

---

## a16z's Counter-Positioning Lens

a16z consistently invests based on counter-positioning theses. Their question: "Why can't the market leader do this?"

The answer must be **structural**, not executional:
- "They're slower" → not structural (they can hire/acquire)
- "They don't care about this segment" → slightly structural (requires deliberate neglect)
- "Their pricing model requires per-seat contracts; our usage-based model would cannibalize 40% of their existing ARR" → structural (changing requires self-harm)
- "They are the incumbent that our customers are trying to escape; being associated with them is a liability" → structural (brand is working against them)
