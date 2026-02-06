# Assumption Testing Principles

Compact reference for identifying, ranking, and testing assumptions before building. Load when working on validation planning, MVP definition, or early-stage product validation.

---

## Core Truth

**Every product idea is a stack of assumptions.** Most fail not because the execution was bad, but because a core assumption was wrong. Find the riskiest assumptions and test them before writing code.

---

## Thinking in Assumptions

### What is an Assumption?

Something that must be true for your product to succeed, but you don't have proof yet.

**Examples:**
- "People will switch from their current solution"
- "Users will pay $99/month for this"
- "The technical approach is feasible at scale"
- "We can acquire customers for less than $100"
- "People will refer their friends"

### The Two Types

**1. Assumptions about DESIRABILITY**
- Do customers want this?
- Will they pay for it?
- Is the problem painful enough?

**2. Assumptions about FEASIBILITY**
- Can we build it?
- Can we scale it?
- Can we support it?
- Can we distribute it?

**Test desirability first.** No point building something feasible that no one wants.

---

## The Assumption Stack

Build your assumption stack explicitly:

```
Our product succeeds IF:
├─ People have problem X (desirability)
├─ Current solutions fail to solve X (desirability)
├─ Our approach solves X better (desirability)
├─ People will pay $Y for the solution (desirability)
├─ We can build it in Z months (feasibility)
├─ We can acquire customers for less than $W (feasibility)
└─ We can scale to N users (feasibility)
```

**Make it exhaustive.** Write down every assumption you're making.

---

## Risk Ranking

Not all assumptions are equally risky. Rank by:

**Impact × Uncertainty = Risk**

### Impact
If this assumption is wrong, what happens?
- **Critical:** Product fails completely
- **High:** Major pivot required
- **Medium:** Delays or scope reduction
- **Low:** Minor adjustment

### Uncertainty
How confident are you this is true?
- **High uncertainty:** Pure guess, no evidence
- **Medium uncertainty:** Some signals, not conclusive
- **Low uncertainty:** Strong evidence, confident

### The Priority Matrix

| Uncertainty | Critical Impact | High Impact | Medium Impact | Low Impact |
|-------------|-----------------|-------------|---------------|------------|
| **High**    | **TEST FIRST**  | Test early  | Test when convenient | Assume true |
| **Medium**  | Test early      | Test soon   | Monitor       | Assume true |
| **Low**     | Validate once   | Monitor     | Assume true   | Assume true |

**Focus on high uncertainty + high impact.** These will kill you if wrong.

---

## Validation Experiments

How to test assumptions cheaply and fast:

### The Experiment Structure

For each assumption to test:
1. **Hypothesis:** "We believe [assumption]"
2. **Test:** "To verify, we will [experiment]"
3. **Success criteria:** "We'll know we're right if [specific result]"
4. **Timeline:** "In [X days/weeks]"

**Example:**
- Hypothesis: "Small business owners will pay $99/mo for this"
- Test: "Create landing page with pricing, run $500 in ads, measure conversion to 'start trial'"
- Success: "5% of visitors sign up for trial"
- Timeline: "2 weeks"

### Validation Hierarchy (Cheapest to Most Expensive)

**1. Customer Conversations**
- Talk to 10-20 people who have the problem
- Ask about current solutions, willingness to pay
- **Cost:** Free
- **Time:** 1-2 weeks
- **Validates:** Problem severity, current alternatives

**2. Landing Page Test**
- Create landing page describing the solution
- Drive traffic (ads, social, communities)
- Measure interest (email signups, pre-orders)
- **Cost:** $500-$2000
- **Time:** 1-2 weeks
- **Validates:** Value prop resonance, rough demand

**3. Prototype/Mockup**
- Build a clickable prototype or demo
- Show to target customers
- Measure willingness to pay or pre-order
- **Cost:** 1-2 weeks of design time
- **Time:** 2-3 weeks
- **Validates:** UX expectations, feature priorities

**4. Concierge MVP**
- Manually deliver the value before building the product
- **Example:** Manually curate recommendations before building algorithm
- **Cost:** High time cost, low dev cost
- **Time:** Ongoing
- **Validates:** Will people pay? Is the value real?

**5. Wizard of Oz MVP**
- Looks like a product, but you're manually operating behind the scenes
- **Example:** "AI" feature that's actually a human
- **Cost:** Moderate dev + high time cost
- **Time:** 2-4 weeks to build, ongoing to operate
- **Validates:** Full product experience, willingness to pay

**6. Working MVP**
- Build the minimum that actually works
- **Cost:** Highest
- **Time:** 4-12 weeks typically
- **Validates:** Everything

**Start at #1. Only move down the list when you've validated the cheaper tests.**

---

## Build-Measure-Learn

The validation loop:

### Build (Minimum)
What's the smallest thing you can build to test the assumption?

**Not:** "Full product with all features"
**Instead:** "One feature that tests the core assumption"

### Measure (Specific)
What metric will tell you if the assumption is true?

**Not:** "See if people like it"
**Instead:** "20% of trial users convert to paid within 30 days"

### Learn (Honest)
What did you learn? Was the assumption validated or invalidated?

**Three outcomes:**
1. **Validated** — Evidence supports the assumption, proceed
2. **Invalidated** — Evidence contradicts, pivot or kill
3. **Inconclusive** — Need more data or different test

**Be honest.** Weak signals aren't validation. "They said they liked it" ≠ "they paid for it."

---

## MVP Scope Definition

**MVP = Minimum Viable Product**

Not "minimum features." Minimum to validate your riskiest assumptions.

### The MVP Formula

1. List all assumptions
2. Rank by risk (uncertainty × impact)
3. Identify the top 3 riskiest assumptions
4. Define the minimum product needed to test those 3 assumptions
5. **That's your MVP scope**

### What to Cut

**Include:**
- Features needed to test core assumptions
- Minimum to deliver core value
- Enough quality that people would actually use it

**Cut:**
- Features that don't test assumptions
- Nice-to-haves
- Optimizations and polish
- Scale/performance beyond what you need for testing

**The test:** "If we remove this, can we still validate our riskiest assumption?"
- If yes: Cut it
- If no: Keep it

---

## Success Criteria

Define what "validated" means BEFORE running the experiment.

### Good Criteria

**Specific and measurable:**
- "10 customers pre-pay for beta access" ✅
- "People seem interested" ❌

**Achievable in timeframe:**
- "5 trial signups in 2 weeks" ✅
- "1000 users in 2 weeks" ❌ (unless you have distribution)

**Meaningful signal:**
- "20% convert to paid" ✅ (revenue validates willingness to pay)
- "100 email signups" ❌ (email is low commitment)

### The Commitment Ladder

Measure commitment, not interest:

1. **Said they like it** — Weakest signal
2. **Gave you their email** — Low commitment
3. **Signed up for trial** — Medium commitment
4. **Used it repeatedly** — High commitment
5. **Paid for it** — Strongest signal
6. **Referred others** — Product-market fit signal

**Optimize for climbing the ladder, not stopping at the bottom.**

---

## Red Flags

**"We'll figure it out as we build"**
- No. Test assumptions before building, not during.

**"If we build it, they will come"**
- Assuming distribution works is the deadliest assumption.

**"Everyone we talked to loved the idea"**
- Did they pay? If not, it's not validation.

**"We need to launch to really know"**
- Launch is the most expensive test. Run cheaper ones first.

**"Our MVP needs these 50 features"**
- That's not an MVP. That's a full product. Cut scope.

---

## The Validation Checklist

Before building:

- [ ] Have we listed all critical assumptions?
- [ ] Have we ranked them by uncertainty and impact?
- [ ] Have we identified the top 3 riskiest assumptions?
- [ ] Have we designed experiments to test them?
- [ ] Have we defined specific success criteria for each test?
- [ ] Have we run the cheapest possible tests first?
- [ ] Are we measuring commitment, not just interest?

If you can't check all boxes, you're not ready to build.

---

## Key Insight

**The goal of validation isn't to prove you're right. It's to find out the truth as cheaply as possible.**

Being wrong quickly is better than being wrong slowly. Test assumptions fast, kill bad ideas faster.
